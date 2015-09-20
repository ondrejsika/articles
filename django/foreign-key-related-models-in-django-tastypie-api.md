---
layout: default
title: Foreign key related models in django-tastypie API
---

[django](.)

# {{ page.title }}


Moved from <https://ondrejsika.com/blog/2014/01/05/foreign-key-related-models-in-django-tastypie-api.html>:

Example models structure in file `example/models.py`

    from django.db import models

    class Gallery(models.Model):
        name = models.CharField(max_length=64)

    class Image(models.Model):
        gallery = models.ForeignKey(Gallery)
        name = models.CharField(max_length=64)
        file = models.ImageField(upload_to="files")

Basic resource class look like this. file `example/api/resources.py`

    from tastypie.resources import ModelResource
    from ..models import Image, Gallery

    class ImageResource(ModelResource):
        class Meta:
            queryset = Image.objects.all()
            allowed_methods = ['get']

    class GalleryResource(ModelResource):
        class Meta:
            queryset = Gallery.objects.all()
            allowed_methods = ['get']

Apis response for `GET /api/v1/gallery/1/?format=json`

    {
        "id": 1,
        "name": "My family",
        "resource_uri": "/api/v1/gallery/1/"
    }

You must add `ToManyField` field to `GalleryResource` class. Firest argument is related resource, second related name.

in file `example/api/resource.py`

    from tastypie.resources import ModelResource
    from tastypie import fields
    from ..models import Image, Gallery

    class ImageResource(ModelResource):
        class Meta:
            queryset = Image.objects.all()
            allowed_methods = ['get']

    class GalleryResource(ModelResource):
        images = fields.ToManyField(ImageResource, 'image_set')
        class Meta:
            queryset = Gallery.objects.all()
            allowed_methods = ['get']

Now return list of image api urls.

    {
        "id": 1,
        "name": "My family",
        "images": [
            "/api/v1/image/1/",
            "/api/v1/image/2/",
        ],
        "resource_uri": "/api/v1/gallery/1/"
    }

If you want list of related object must set third parameter `full=True`.

    images = fields.ToManyField(ImageResource, 'image_set', full=True)

Now response include full related objects

    {
        "id": 1,
        "name": "My family",
        "images": [
            {
                "name": "My parrents",
                "file": "/static/uploads/files/myparrents.jpg",
                "resource_uri": "/api/v1/image/1/"
            },
            {
                "name": "My with dog",
                "file": "/static/uploads/files/mewithdog.jpg",
                "resource_uri": "/api/v1/image/2/"
            }
        ],
        "resource_uri": "/api/v1/gallery/1/"
    }


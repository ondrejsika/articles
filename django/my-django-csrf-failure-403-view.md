---
layout: default
title: My Django CSRF failure (403) view
---

[django](.)

# {{ page.title }}


Moved from <https://ondrejsika.com/blog/2014/05/18/my-django-csrf-failure-403-view.html>:

add path to view to settings

    CSRF_FAILURE_VIEW = 'views.csrf403'

create simple view

    from django.shortcuts import render

    def csrf403(request, reason):
        return render(request, '403csrf.html', {'reason': reason})

or view with sentry logging

    from django.shortcuts import render

    import logging
    from raven.contrib.django.models import client

    def csrf403(request, reason):
        data = client.get_data_from_request(request)
        data.update({
            'level': logging.WARN,
            'logger': 'http403',
        })
        result = client.captureMessage(message='CSRF error: %s %s' % (reason, request.build_absolute_uri()), data=data)
        request.sentry = {
            'project_id': data.get('project', client.project),
            'id': client.get_ident(result),
        }
        return render(request, '403csrf.html')


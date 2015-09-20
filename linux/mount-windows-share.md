---
layout: default
title: Mount Windows Share
---

[linux](.)

# {{ page.title }}

Intall cifs utils

    sudo apt-get install cifs-utils

Mount (example) where stor.bo is a hostname, share is a share name and sika is my user

    sudo mount -t cifs -o uid=sika -o gid=sika //stor.bo/share /mnt/stor_bo/



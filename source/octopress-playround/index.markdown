---
layout: page
title: "Octopress Playround"
date: 2013-12-26 23:05
comments: true
sharing: true
footer: true
---

### Clone về máy nhà

    git clone --branch=source git@github.com:andytruong/andytruong.github.io.git andytruong.github.io.git
    cd andytruong.github.io.git

### Publish changes
    rake generate; rake deploy

### Vừa soạn bài vừa coi kết quả

    rake watch . &; cd public/andytruong; php -S 127.0.0.1:4000

### Refresh hoài mà không thấy nội dung cập nhật

    rake generate

### Nhúng gist vào bài viết

    {% raw %}
      {% gist 8052716 %}
    {% endraw %}

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

### [Nhúng code sử dụng codeblock](http://octopress.org/docs/plugins/codeblock/)

{% codeblock Coffeescript Tricks lang:coffeescript start:51 mark:51,54-55 %}
# Given an alphabet:
alphabet = 'abcdefghijklmnopqrstuvwxyz'

# Iterate over part of the alphabet:
console.log letter for letter in alphabet[4..8]
{% endcodeblock %}

{% codeblock PHP Tricks lang:php start:51 mark:51,54-55 %}
function say_hello($name = 'Andy Truong') {
  return "Hello {$name}";
}

say_hello();
{% endcodeblock %}

### Use backtick

``` coffeescript Coffeescript Tricks start:51 mark:52,54-55
# Given an alphabet:
alphabet = 'abcdefghijklmnopqrstuvwxyz'

# Iterate over part of the alphabet:
console.log letter for letter in alphabet[4..8]
```

``` php Demo PHP
function say_hello($name = 'Andy Truong') {
  return "Hello {$name}";
}

say_hello();
```

### [Use include_code](http://octopress.org/docs/plugins/include-code/)

This is the best way ;)

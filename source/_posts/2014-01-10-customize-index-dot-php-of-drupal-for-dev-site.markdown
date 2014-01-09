---
layout: post
title: "Customize index.php of Drupal for Dev site"
date: 2014-01-10 00:41:36 +0700
comments: true
categories: ['Drupal', 'Drupal 7', 'Debug']
---

Tôi chỉ apply hack này ở môi trường dev, để tiện theo dõi các lỗi xảy ra nếu có,
và đo đạc hiệu năng sử dụng XHProf.

<!-- more -->

{% include_code Customized index.php for Drupal Development environment lang:php php/drupal/7/index.php %}

**Khi này:**

- Nếu có lỗi thì đoạn catch() sẽ chụp và in trace() rõ ràng.
- Nếu tôi muốn hiển thị thông tin profile từ xhprof thì tôi thêm tham số
  `/?go_profile=1` vào URL

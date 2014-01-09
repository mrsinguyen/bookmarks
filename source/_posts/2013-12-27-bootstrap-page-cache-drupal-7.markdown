---
layout: post
title: "Bootstrap page cache - Drupal 7"
date: 2013-12-27 16:10:17 +0700
comments: true
categories: ['Drupal', 'Drupal 7', 'bootstrap', 'cache']
---

Hôm nay, tôi có đụng tới phần cache của cái bộ route trong Drupal 7, nên muốn đi
coi kỹ lại phần bootstrap của Drupal.

<!-- more -->

Bootstrap của Drupal 7 gồm có các bước sau, tui chỉ copy lại từ phần comment của
hàm drupal_bootstrap() thôi.

* **DRUPAL_BOOTSTRAP_CONFIGURATION**: Initializes configuration.
* **DRUPAL_BOOTSTRAP_PAGE_CACHE**: Tries to serve a cached page.
* **DRUPAL_BOOTSTRAP_DATABASE**: Initializes the database layer.
* **DRUPAL_BOOTSTRAP_VARIABLES**: Initializes the variable system.
* **DRUPAL_BOOTSTRAP_SESSION**: Initializes session handling.
* **DRUPAL_BOOTSTRAP_PAGE_HEADER**: Sets up the page header.
* **DRUPAL_BOOTSTRAP_LANGUAGE**: Finds out the language of the page.
* **DRUPAL_BOOTSTRAP_FULL**: Fully loads Drupal. Validates and fixes input data.

Mấy phần khác tui không quan tâm lắm, tui chỉ quan tâm tới cái bước
DRUPAL_BOOTSTRAP_PAGE_CACHE. Nghĩa là để cho Drupal delivery được nội dung
tới người dùng cuối mà không có đụng tới DB, tui cần phải làm gì. Tui coi tới
coi lui, thì tạm kết luận, cái luồng của nó như sau:

- _drupal_bootstrap_page_cache()
- If variable_get('page_cache_without_database'),
  - then $conf['cache'] is true. There is no DB bootstrap here.
  - else, force drupal boots DRUPAL_BOOTSTRAP_DATABASE and DRUPAL_BOOTSTRAP_VARIABLES
- If !$conf['cache'], no page cache, boot to next step.
- If User IP is block, return 403, exit -- drupal_is_denied() only query db if db
  connection is available
- If user has cookie, or the request is not cachable
  - Then, header has 'X-Drupal-Cache: MISS'
  - Else, get cached content
    - Cache ID: $base_root . request_uri()
    - Cache Bin: cache_page
    - Cachable: Http Method = GET/HEAD, !drupal_is_cli()
    - Cached data must be array(), has key path, title, …
    - If $conf['page_cache_invoke_hooks'] > invoke hook_boot
    - Delivery content -- drupal_serve_page_from_cache($cache)
    - If $conf['page_cache_invoke_hooks'] > invoke hook_exit

Vậy thôi, hy vọng note này giúp ích gì đó cho người tìm kiếm trên Google.

**Vợ Ba Con**

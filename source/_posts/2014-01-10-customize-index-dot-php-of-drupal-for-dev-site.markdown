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

{% codeblock Customized index.php for Drupal Development environment lang:php %}

define('DRUPAL_ROOT', getcwd());

require_once DRUPAL_ROOT . '/includes/bootstrap.inc';
drupal_bootstrap(DRUPAL_BOOTSTRAP_FULL);

try {
  if (!empty($_GET['go_profile'])) {
    xhprof_enable();
  }

  menu_execute_active_handler();

  if (!empty($_GET['go_profile'])) {
    $xhprof_data = xhprof_disable();

    $XHPROF_ROOT = "/var/www/";
    include_once $XHPROF_ROOT . "/xhprof_lib/utils/xhprof_lib.php";
    include_once $XHPROF_ROOT . "/xhprof_lib/utils/xhprof_runs.php";

    $xhprof_runs = new XHProfRuns_Default();
    $run_id = $xhprof_runs->save_run($xhprof_data, $_SERVER['SERVER_NAME']);

    echo '<a href="http://xhprof.da.go1.com.vn/index.php?run=', $run_id, '&source=', $_SERVER['SERVER_NAME'], '">XHProf #', $run_id, '</a>';
  }
}
catch (Exception $e) {
  $p = function_exists('kpr') ? 'kpr' : 'print_r';
  $p($e->getMessage());
  $p($e->getTrace());
}
{% endcodeblock %}

**Khi này:**

- Nếu có lỗi thì đoạn catch() sẽ chụp và in trace() rõ ràng.
- Nếu tôi muốn hiển thị thông tin profile từ xhprof thì tôi thêm tham số
  `/?go_profile=1` vào URL

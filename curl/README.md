#### Post data

    curl --data "param1=value1&param2=value2" http://example.com/resource.cgi

#### Upload file

Example 1

    curl -XPUT http://127.0.0.1:8098/riak/images/drupal.jpg \
      -H "Content-type: image/jpeg" \
      --data-binary @/var/aegir/host_master/004/misc/druplicon.png

Example 2

    curl --form "fileupload=@filename.txt" http://example.com/resource.cgi

#### Custom method

    curl -X POST -d @filename http://example.com/path/to/resource --header "Content-Type:text/xml"

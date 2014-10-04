#### Post data

    curl http://example.com/resource.cgi \
        -X POST \
        --data "param1=value1&param2=value2"

#### Upload file

Example 1

    curl http://127.0.0.1:8098/riak/images/drupal.jpg \
      -X PUT \
      -H "Content-type: image/jpeg" \
      --data-binary @/var/aegir/host_master/004/misc/druplicon.png

Example 2

    curl http://example.com/resource.cgi \
        --form "fileupload=@filename.txt"

#### Custom method

    curl http://example.com/path/to/resource \
        -X POST \
        -H "Content-Type:text/xml" \
        --data "param1=value1&param2=value2"

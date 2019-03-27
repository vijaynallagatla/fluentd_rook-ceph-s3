# Rook's Ceph S3 storage Add-On integration with Fluentd
s3 output plugin buffers event logs in local file and upload it to S3 periodically.

```
$ gem install fluent-plugin-s3 -v "~> 0.8" --no-document # for fluentd v0.12 or later
$ gem install fluent-plugin-s3 -v 1.0.0 --no-document # for fluentd v1.0 or later
```
Create a fluentd local docker image with fluentd-ceph-s3-image/Dockerfile

```
gem 'fluent-plugin-s3', '~>1.0.0' // this installs S3 plugin needed for fluentd output plugin
```

Fluentd ConfigMap
-----------------
Add following Output conf replacing the {{ . }} with corresponding configuration values. (File - fluentd-ceph-s3-configmap.yaml)

```
<match **>
      @type s3
      aws_key_id {{.CEPH_S3_KEY_ID}}
      aws_sec_key {{.CEPH_S3_SECRET_KEY}}
      s3_bucket {{.CEPH_S3_BUCKET_NAME}}
      s3_endpoint {{.CEPH_S3_URL_WITH_STORE_NAME}}
      path logs
      # by default Objects are gZipped but you can store as json
      store_as json
      <buffer tag,time>
        @type file
        path /var/log/fluent/s3
        timekey 3600 # 1 hour partition
        timekey_wait 10m
        timekey_use_utc true # use utc
        chunk_limit_size 256m
      </buffer>
    </match>
    ```

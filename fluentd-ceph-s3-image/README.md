# Collecting Docker Log Files with Fluentd and Rook's Ceph S3 / AWS S3 storage
This directory contains the source files needed to make a Docker image
that collects Docker container log files using [Fluentd][fluentd]
and sends them to an instance of [Elasticsearch][elasticsearch].
This image is designed to be used as part of the [Kubernetes][kubernetes]
cluster bring up process. The image resides at GCR under the name
[k8s.gcr.io/fluentd-elasticsearch][image].

[fluentd]: http://www.fluentd.org/
[S3]: https://docs.fluentd.org/v1.0/articles/out_s3
[kubernetes]: https://kubernetes.io

[![Analytics](https://kubernetes-site.appspot.com/UA-36037335-10/GitHub/cluster/addons/fluentd-elasticsearch/fluentd-es-image/README.md?pixel)]()

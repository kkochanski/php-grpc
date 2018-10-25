PHP-GRPC
=================================
[![Latest Stable Version](https://poser.pugx.org/spiral/php-grpc/version)](https://packagist.org/packages/spiral/php-grpc)
[![GoDoc](https://godoc.org/github.com/spiral/php-grpc?status.svg)](https://godoc.org/github.com/spiral/php-grpc)
[![Build Status](https://travis-ci.org/spiral/php-grpc.svg?branch=master)](https://travis-ci.org/spiral/php-grpc)
[![Go Report Card](https://goreportcard.com/badge/github.com/spiral/php-grpc)](https://goreportcard.com/report/github.com/spiral/php-grpc)
[![Codecov](https://codecov.io/gh/spiral/php-grpc/branch/master/graph/badge.svg)](https://codecov.io/gh/spiral/php-grpc/)

PHP-GRPC is an open-source (MIT licensed) high-performance PHP GRPC server build at top of [RoadRunner](https://github.com/spiral/roadrunner).
Server support both PHP and Golang services running within one application. 

Features:
--------
- native Golang GRPC implementation compliant
- minimal configuration, plug-and-play model
- very fast, low footprint proxy
- simple TLS configuration
- debug tools included
- middleware and server customization support
- code generation using `protoc` plugin (`go get github.com/spiral/php-grpc/cmd/protoc-gen-php-grpc`)
- transport, message, worker error management
- response error codes over php exceptions
- works on Windows

Usage:
--------
Install `rr-grpc` and `protoc-gen-php-grpc` by building it or use [pre-build binaries](https://github.com/spiral/php-grpc/releases).

Define your service schema using proto file. You can scaffold protobuf classes and GRPC [service interfaces](https://github.com/spiral/php-grpc/blob/master/example/server/src/Service/EchoInterface.php) using:

```
$ protoc --php_out=target-dir/ --php-grpc_out=target-dir/ sample.proto
```

> Make sure to install [prococ compiler](https://github.com/protocolbuffers/protobuf) and run `composer require spiral/php-grpc` first

[Implement](https://github.com/spiral/php-grpc/blob/master/example/server/src/EchoService.php) needed classes and create [worker.php](https://github.com/spiral/php-grpc/blob/master/example/server/worker.php) to invoke your services.

Place [.rr.yaml](https://github.com/spiral/php-grpc/blob/master/example/server/.rr.yaml) (or any other format supported by viper configurator) into the root of your project. You can run your application now:

```
$ rr-grpc serve -v -d
```

To reset workers state:

```
$ rr-grpc grpc:reset
```

To show workers statistics:

```
$ rr-gprc grpc:workers -i
```

> See [example](https://github.com/spiral/php-grpc/tree/master/example).

You can find more details regarding server configuration at [RoadRunner Wiki](https://github.com/spiral/roadrunner/wiki).

License:
--------
The MIT License (MIT). Please see [`LICENSE`](./LICENSE) for more information. Maintained by [SpiralScout](https://spiralscout.com).

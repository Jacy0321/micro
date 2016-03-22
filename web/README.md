# Micro Web

Micro web provides a visual point of entry for the micro environment and should replicate 
the features of the CLI.

## Features

Feature	|	Description
---	|	---
UI	|	A dashboard to view and query running services
Proxy	|	A reverse proxy to micro web services (includes websocket support)

### Proxy

Micro Web has a built in HTTP reverse proxy for micro web apps. This essentially allows you 
to treat web applications as first class citizens in a microservices environment. The proxy 
will use /[service] along with the namespace (default: go.micro.web) to lookup the service 
in service discovery. It composes service name as [namespace].[name]. 

The proxy will strip /[service] forwarded the rest of the path to the web app. It will also 
set the header "X-Micro-Web-Base-Path" to the stripped path incase you need to use it for 
some reason like constructing URLs.

Example translation

Path	|	Service	|	Service Path	|	Header: X-Micro-Web-Base-Path
---	|	---	|	---	|	---
/foo	|	go.micro.web.foo	|	/	|	/foo
/foo/bar	|	go.micro.web.foo	|	/bar	|	/foo


## Getting Started

### Install
```bash
go get github.com/micro/micro
```

### Run Web UI/Proxy

```bash
micro web
```
Browse to localhost:8082

### Serve Secure TLS

The Web proxy supports serving securely with TLS certificates

```bash
micro --enable_tls --tls_cert_file=/path/to/cert --tls_key_file=/path/to/key web
```

### Set Namespace

The Web defaults to serving the namespace **go.micro.web**. The combination of namespace and request path 
are used to resolve a service to reverse proxy for.

```bash
micro --web_namespace=com.example.web
```

## Stats

You can enable a stats dashboard via the `--enable_stats` flag. It will be exposed on /stats.

```shell
micro --enable_stats web
```

<img src="https://github.com/micro/micro/blob/master/doc/stats.png">

## Screenshots

<img src="https://github.com/micro/micro/blob/master/web/web1.png">
-
<img src="https://github.com/micro/micro/blob/master/web/web2.png">
-
<img src="https://github.com/micro/micro/blob/master/web/web3.png">


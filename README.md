# proxy3

HTTP/HTTPS proxy in a single python script


## Features
* python3 support
* easy to customize
* require no external modules
* support both of IPv4 and IPv6
* support HTTP/1.1 Persistent Connection
* support dynamic certificate generation for HTTPS intercept

You need to install OpenSSL to intercept HTTPS connections.


## Usage

Just run as a script:

```
$ python3 proxy3.py
```

Above command runs the proxy on localhost:8080.
Verify it works by typing the below command on another terminal of the same host.

```
$ http_proxy=localhost:8080 curl http://www.example.com/
```

proxy3 is made for debugging/testing, so it only accepts connections from localhost.

To use another port, specify the port number as the first argument.

```
$ python3 proxy3.py 3128
```


## Enable HTTPS intercept

To intercept HTTPS connections, generate private keys and a private CA certificate:

```
$ ./setup_https_intercept.sh
```

Through the proxy, you can access http://proxy2.test/ and install the CA certificate in the browsers.


## Customization

You can easily customize the proxy and modify the requests/responses or save something to the files.
The ProxyRequestHandler class has 3 methods to customize:

* request_handler: called before accessing the upstream server
* response_handler: called before responding to the client
* save_handler: called after responding to the client with the exclusive lock, so you can safely write out to the terminal or the file system

By default, only save_handler is implemented which outputs HTTP(S) headers and some useful data to the standard output.

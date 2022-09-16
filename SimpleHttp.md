# Simple Http Server

The simple http server is a minimal http server created for testing purposes. It was introduced in Java 18 and I found it easy to use and 
handy. Here is what it can do.

## Goals [[2](https://openjdk.org/jeps/408)] :

* Offer an out-of-the-box static HTTP file server with easy setup and minimal functionality.

* Reduce developer activation energy and make the JDK more approachable.

* Provide a default implementation via the command line together with a small API for programmatic creation and customization.

## How to use it:

It is possible to run SimpleHttpServer from the command line and Java code. Here is the way we can call it from the command line [[1](https://blogs.oracle.com/javamagazine/post/java-18-simple-web-server)]:

```Bash
$ jwebserver [-b bind address] [-p port] [-d directory]
             [-o none|info|verbose] [-h to show options]
             [-version to show version information]
```

Options are:
* -h or -? or --help: Prints the help message and exits.
* -b addr or --bind-address addr: Specifies the address to bind to. The default is 127.0.0.1 or ::1 (loopback). For all interfaces, use -b 0.0.0.0 or -b ::
* -d dir or --directory dir: Specifies the directory to serve. The default is the current directory.
* -o level or --output level: Specifies the output format. The levels are none, info, and verbose. The default is info.
* -p port or --port port: Specifies the port to listen on. The default is 8000.
* -version or --version: Prints the Simple Web Server’s version information and exits.

## TODO (Code examples)


### References:
1. [https://blogs.oracle.com/javamagazine/post/java-18-simple-web-server](https://blogs.oracle.com/javamagazine/post/java-18-simple-web-server)
2. [https://openjdk.org/jeps/408](https://openjdk.org/jeps/408)

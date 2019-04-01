# Web

## Background knowledge

### IP

IP protocol, which is really the lowest level abstraction above the hardware. _Please distinguish IP protocol from ethernet, wireless, or any other physical networking mechanism._This is a data protocol that sits on top of some physical network.

**IP** is an addressing and fragmentation protocol:

- It breaks all communications into _packets_, chunks of data up to 65536 bytes long.
- Packets are individually _routed_ from source to destination.
- IP is allowed to drop packets; i.e., it is an unreliable protocol.
- There are no acknowledgements and no retransmissions.
- There is no flow-control saying "_You're sending data too fast!_"

### IP Address

IP uses _IP addresses_ to define source/target. IPs are 32 bit numbers represented as 4 8-bit numbers separated by periods. Eg. When you try to visit `www.cnn.com` in your browser, the computer must first translate `www.cnn.com` to an IP address. Then the browser can make a connection to the web server on the target machine identified by the IP address. 

There are some special IPs:

- Behind firewalls, people often use 192.168.x.y and use NAT \(_network address translation_\) in their firewall to translate an outside address \(a real IP\) to the special IPs behind the wall. In this case there is an external or public IP address and a private IP address. My `varmint.cs.usfca.edu` machine has public IP 138.202.170.154 but internal IP 10.10.10.51 or something like that.
- 127.0.0.1 is `localhost` or "my machine"

### DNS Domain Name Service

DNS is a distributed database that maps domain names to IP addresses using a series of distributed DNS servers. It is really just a dictionary that maps a name to an IP address.

### TCP/IP

TCP \(_Transmission Control Protocol_\) is another protocol, a reliable but slower one, sitting on top of IP. Believe it or not it comes from the 1970s. Characteristics:

- Reliable \(fault tolerant\). TCP automatically deals with lost packets before delivering a complete "file" to a recipient.
- Stream-oriented connections. We can treat the connection like a stream/file rather than packets.
- Packets are ordered into the proper sequence at the target machine via use of _sequence numbers_.
- Control-flow prevents buffer overflows etc...

### Socket

If the IP address is like an office building's main phone number, sockets are like the extension numbers for offices and are often called the _port_. So the IP and socket uniquely identify an "office" \(server process\). We open sockets to these ports in order to communicate with servers.

Ports range from 1..65535. 1..1024 require root/superuser privileges to use and ports 1..255 are reserved for common, publicly-defined server ports like:

- 80: HTTP \(web\)
- 110: POP \(mail\)
- 25: SMTP \(mail\)
- 22: SSH \(remote shell connections\)

You can use `telnet` \(`putty` on windows\) to connect to remote ports to manually speak the protocol.

```text
$ telnet www.usfca.edu 80
Trying 104.239.221.147...
Connected to www.usfca.edu.
Escape character is '^]'.
```

### Server vs Client

A server listens for connection requests from clients across the network or even from the same machine. Clients know how to connect to the server given an **IP address and port number**.

### HTTP

HTTP is the text-based protocol used to pass information between browser and server over the Internet.

Here is the protocol for handshaking with the Web server:

```text
GET / HTTP/1.1
Host: www.cnn.com

```

The first line tells the server what page we are interested in \(the root `/`\). The `Host:` line indicates what server we think we are talking to. Then, we have to have a blank line which indicates we are done talking/handshaking. Please try out this sample session:

```text
$ telnet www.antlr.org 80
Trying 151.101.41.67...
Connected to ...
Escape character is '^]'.
GET / HTTP/1.1
Host: www.antlr.org

```

The server responds to you with:

```text
HTTP/1.1 200 OK
access-control-allow-origin: *
cache-control: max-age=60
...
Set-Cookie: countryCode=US; Domain=.cnn.com; Path=/
Set-Cookie: geoData=San Jose|CA|95113|US|NA; Domain=.cnn.com; Path=/
Content-Type: text/html; charset=utf-8
Date: Sat, 08 Apr 2017 17:55:36 GMT

<!DOCTYPE html>
<html class="no-js">
<head>
...
</head>
...
</html>
```

It sends us back some headers, such as `Content-Type` and `Date`. Also, please note that _cookies_ come back from the server to your web browser using these headers.

### Cookie

HTTP is stateless and anonymous with a very simple request-response model. In order to build websites like Amazon or any other website that lets you login, we need a mechanism for identifying users that come back to the same server. By identifying, we mean recognizing the same "client," not actually knowing who they are.

HTTP is pretty simple but ~20 years ago, we came up with a good idea to support stateful communications between client and server. The idea is to piggyback key-value pairs called _cookies_ as regular old headers already allowed within the HTTP protocol. These key-value pairs therefore do not affect the data payload \(stuff after the headers\).

The cookie mechanism relies on a simple agreement between client and server. The sequence goes like this when a client visits a server for the first time:

1. Server sends back one or more cookies to the browser via headers
2. Browser saves this information and then sends the same data back to the server for every future request associated with that domain/server

A _cookie_ is a named piece of data \(string\) associated with a specific website/URL that is saved by the browser and is sent back to that same server with every page request. The server can use that as a key to retrieve data associated with that user.

Your browser keeps a dictionary of cookies for each server. If you have 3 browsers, each would keep a separate dictionary. If you erase your browser cookies for that domain, the server will no longer recognize you. Naturally, the server will try to send you cookies again. It is up to the browser to follow the agreement to keep sending cookies and to save data.

Can I, as a server, ask for another server's cookies \(such as amazon.com's\)? No! Security breach! If another server can get my amazon cookies, the other server/person can log in as me on amazon. Heck, my cookies might even store credit card numbers \(bad idea\). It is up to the browser to enforce this policy. Naturally, it could send every cookie or even every document on your computer via headers to a server! In essence, we are trusting browser implementors.

A server can specify the lifetime of cookies in terms of seconds to live or that cookie should die when the browser closes. It can also tell the browser to delete a cookie immediately as part of the current request.

#### Ad companies track via cookies



## Get webpages

### Using python requests package

Usually we will use `requests`:

```text
import requests
r = requests.get('http://www.cnn.com')
print(r.text)
```

### Using python urllib2 package

Optionally, we can use `urllib2`:

```text
import urllib2
response = urllib2.urlopen("http://www.cnn.com")
html = response.read()
print(html)
```

### Under command line

If we want to do it without python:

```text
$ curl https://www.cnn.com > cnn.html
# Or
$ wget -O cnn.html https://www.cnn.com
```

## Using python to create web server

Making a web server in Python is fairly easy if we use, yet another library, [Flask](http://flask.pocoo.org/). Flask provides _annotations_ that **map URL paths to Python functions**. Every URL for which you want the server to respond, requires an annotation/function combination.

### Hello Flask

```text
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello MSAN692!\n"

app.run()
```

The default flask server listens at port 5000. To contact the server, we need the address of the machine, just our local host, and the port: 127.0.0.1:5000.

### Add parameter

```text
@app.route("/hello/<name>")
def hello(name):
    return "Hello %s!\n" % name
```

### Accept URLs with an argument

Update server so that it accepts URLs with an _argument_, `/data?format=txt`, and gives html by default or csv if `txt` format.

```text
from flask import request
...
mydata = """parrt, 10, 134.983
tombu, 11, 99.001
"""
mydata_html = """
<b>parrt</b>, 10, 134.983<br>
tombu, 11, 99.001
"""
...
@app.route("/data")
def foo():
    if request.args.get("format")=='txt':
        return mydata
    else:
        return mydata_html
```

### Set cookies

```text
@app.route('/setcookie')
def cookie_insertion():
    response = app.make_response("i set some cookies. haha!\n")
    response.set_cookie('ID',value='212392932')
    return response
```

### Fetch cookies

```text
@app.route('/getcookie')
def getcookie():
   name = request.cookies.get('ID')
   return '<h1>Welcome ID '+name+'</h1>'
```

### Kill cookies

```text
response.set_cookie(name, expires=0)
```

### Redirect browser

```text
@app.route('/')
def root():
    return redirect('/homepage')

@app.route('/homepage')
def homepage():
    return "<h1>Home page</h1>"
```


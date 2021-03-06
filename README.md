# Dwight Conrad

![dwight](http://www.netbrawl.com/uploads/93be3b042e6765ed83a95fa8b8949406.JPG)

Dwight is [3scale](http://www.3scale.net) answer to the need of routing HTTP/HTTPS traffic between different stacks. It is also used when we need to release new features to a selective group of users or when we need to move certain percentage of our customers to a new stack for maintenance reasons without losing the power to send them back to the old one. Heavily based on Openresty [DynamicRoutingBasedOnRedis](http://openresty.org/#DynamicRoutingBasedOnRedis)

Dwight is also the smallest son of `Hermes Conrad`, our Routing system on [APItools](http://www.apitools.com), which is in charge of routing traffic between Docker Containers.

# Scenario

![](docs/dwight.png)

# Dependencies

* [Redis](http://redis.io)
* [Openresty](http://openresty.org/) 

# Install Guide

## Install Openresty

```
cd /usr/src
wget http://openresty.org/download/ngx_openresty-1.5.12.1.tar.gz
tar -zxvf ngx_openresty-1.5.12.1.tar.gz
cd ngx_openresty-1.5.12.1
adduser nginx
./configure --prefix=/opt/openresty --with-http_gunzip_module --with-luajit --with-http_ssl_module --with-http_realip_module -j2
make && make install
```

## Install redis

* From source

```
cd /ust/src
wget http://download.redis.io/releases/redis-2.8.12.tar.gz
tar -zxvf redis-2.8.12.tar.gz
cd redis-2.8.12
make
```

* APT (DEBIAN/UBUNTU)

`apt-get install redis-server`

## Install Dwight Conrad

* Clone this repo on your home
```
git clone git@github.com:3scale/dwight-conrad.git /home/${USERNAME}/dwight-conrad
```

* Create directories
````
mkdir -p /opt/openresty/nginx/lua
mkdir -p /opt/openresty/nginx/conf/sites-enabled
ln -s /opt/openresty/nginx/lua/conrad /home/${USERNAME}/dwight-conrad/lua/conrad
ln -s /opt/openresty/nginx/html/conrad /home/${USERNAME}/dwight-conrad/html/conrad
ln -s /opt/openresty/nginx/conf/sites-enabled/conrad /home/${USERNAME}/conrad/sites-enabled/conrad
```

## Set keys in Redis

```
bender@server01:~# redis-cli
127.0.0.1:6379> set "domain.example.com" "proxypass_name"
```

# Feedback

* IRC: `#3scale` on Freenode
* Twitter: `@3scale`

# LICENSE

Copyright (c) 2014 3scale

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

# Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
to

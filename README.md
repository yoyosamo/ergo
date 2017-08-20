
# Ergo [![Build Status](https://travis-ci.org/cristianoliveira/ergo.svg?branch=master)](https://travis-ci.org/cristianoliveira/ergo)

<p align="left" >
<img src="https://s-media-cache-ak0.pinimg.com/736x/aa/bc/3b/aabc3b2b789f478ffb87ac2f0bdd2d33--ergo-proxy-manga-anime.jpg" width="250" align="center" />
<span>Ergo Proxy - The local proxy agent for multiple services development</span>
</p>

The management of multiple apps running over different ports made easy. Create custom local domains for your dev environment.

The Ergo's goal is to be a simple reverse proxy that follows the [unix philosophy](https://en.wikipedia.org/wiki/Unix_philosophy) of doing only one thing and do it well.

Simplicity means no magic involved. Just a flexible reverse proxy that extends the well-known `/etc/hosts` declaration.

**Disclaimer**

This project is under development but it's already usable. Feel free to give me
feedback and opening issues. Suggestions and contributions are welcome. :)

## Why?

When dealing with multiple apps locally is really annoying having to remember each port that represents each service and it gets even worse when you have microservices. So I wanted a simple way to give a proper local domain for each app. Ergos comes to solve this simple problem.

It doesn't aim to be fancy. It solves this problem and nothing else.
Do you want a web interface? You can either try another project or create it
on top of ergo's interface. That's the magic of the Unix philosophy, composition. :D

## Installation

### OSX using brew
```
brew tap cristianoliveira/tap
brew install ergo
```

### Linux / Others using scripts
```
curl -s https://raw.githubusercontent.com/cristianoliveira/ergo/master/install.sh | sh
```

### Using golang
```
go install github.com/cristianoliveira/ergo
```
Make sure you have `$GOPATH/bin` in your path. `export PATH=$PATH:$GOPATH/bin`

## Usage

Ergo looks for a `.ergo` file inside the current folder. It must contain the names and URL of the services following the same format as the `/etc/hosts` (domain+space+url) the main difference is that it also considers the port specified.

**Set the `http://127.0.0.1:2000/proxy.pac` configuration on your system network config (Details below)**

Let's start:
```
echo "ergoproxy http://localhost:3000" > .ergo
ergo run
```
Now you are able to access: `http://ergoproxy.dev`.
Ergo redirects anything that finish with `.dev` to the configured url.

Simple right? No magic involved.

Do you want add more services? So is easy, just add more lines in `.ergo`:
```
echo "otherservice http://localhost:5000" >> .ergo
ergo run
```

Restart the server and access: `http://otherservice.dev`

More you can see in [examples](https://github.com/cristianoliveira/ergo/tree/master/examples)

## Configuration

In order to leave Ergo manage your domains you need to set it as a proxy. Set the `http://127.0.0.1:2000/proxy.pac` on:

##### OS X

`Network Preferences > Advanced > Proxies > Automatic Proxy Configuration`

##### Windows

`Settings > Network and Internet > Proxy > Use setup script`

##### Linux

On Ubuntu

`System Settings > Network > Network Proxy > Automatic`

For other distributions, check your network manager and look for proxy configuration. Use browser configuration as an alternative.

### Browser configuration

Browsers can be configured to use a specific proxy. Use this method as an alternative to system-wide configuration.

##### Chrome

Exit Chrome and start it using the following option:

```sh
# Linux
$ google-chrome --proxy-pac-url=http://localhost:2000/proxy.pac

# OS X
$ open -a "Google Chrome" --args --proxy-pac-url=http://localhost:2000/proxy.pac
```

# License

MIT

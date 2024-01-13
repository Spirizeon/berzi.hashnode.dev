---
title: "Host your own search-engine"
datePublished: Tue Apr 04 2023 10:03:39 GMT+0000 (Coordinated Universal Time)
cuid: clg23eoc3000409m9ho3j8tnz
slug: host-your-own-search-engine
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1680602570264/431bb8b3-b1a9-4338-b5f5-973757857e50.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1680602606266/68c1e8ea-00ce-4696-b61d-3f4af48ed4eb.png
tags: search-engines, searxng

---

Let's host an actual search engine that's free from tracking and ads. We'll be using a Debian machine to do this.

CAUTION! This isn't about making your search engine from scratch but hosting one from pre-existing open-sourced code of [SearXNG](https://github.com/searxng/searxng).

## What is SearXNG

SearXNG is a free internet metasearch engine that aggregates results from various search services and databases. Users are neither tracked nor profiled.

## Requirements

* Linux environment
    
* Docker-compose
    
* Internet-connection
    

## Getting started

Copy the script below into a bash file or directly into your terminal

### Debian/Ubuntu-based distributions

```bash
sudo apt install docker-compose 
cd $HOME
cd /usr/local/searxng-docker
```

If you're on a cloud server, do open the `.env`file and replace the `HOST-NAME` with your machine's domain name.

If you're on a cloud server, do open the `.env`file and replace the `HOST-NAME` with your machine's domain name.

```bash
sudo docker-compose up -d
```

this will start your search engine, if you're doing this on your machine, go to `localhost` on your browser and check it out. To put it down once you're done playing, type this.

```bash
sudo docker-compose down
```

### [Acknowledgement: NetworkChuck](https://www.youtube.com/watch?v=ifT6npY39Dw)

---

### Side note: Please host your search engine files on an offsite server for best privacy practices. Enjoy!
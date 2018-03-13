## **REST**HEART
## The Web API for MongoDB

This is a premade stack designed to reduce friction on adopt MongoDB with **REST**Heart.

## Releases and Release Notes
[![Latest release](https://img.shields.io/github/release/docker-gallery/RESTheart.svg)](https://github.com/docker-gallery/RESTheart/releases/latest) 
[![GitHub Release Date](https://img.shields.io/github/release-date/docker-gallery/RESTheart.svg)](https://github.com/docker-gallery/RESTheart/releases/latest)

[All releases](https://github.com/docker-gallery/RESTheart/releases) 

### Stack Services
* MongoDB (without authentication)
* **REST**Heart

### Configuration
```
--git@github.com:docker-gallery/RESTheart.git
 |--docker-compose.yml (1)
 |--readme.md
 |--restheart 
    |--config
       |--restheart.yml (2)
       |--security.yml (3)
```

#### 1 - docker-compose.yml
Docker Compose file used do declare configurations about both services (restheart and mongodb).

#### 2 - restheart.yml
Used to configure **REST**Heart.

Take a look at line 69: `mongo-uri: mongodb://mongodb` defines a connectionstring to worj with mongodb.

#### 3 - security.yml
Used to configure authentication and authorization on **REST**Heart, by default i've produced some rules, like:
* Anonymus Uses can only read the `publicdb` database data (only if you create the database with name `publicdb`).
* User `admin` user has password `admin`, they has `admins` role and can do everything.
* User `user` user has password `user`, they has `users` role and can do everything only on `publicdb`.


# Get Started

* On any docker environment
* There we go! `
Run 
```
git clone https://github.com/docker-gallery/RESTheart.git
cd ./RESTheart
docker-compose up
```
Just it. 


## Read More

[Wiki](https://github.com/docker-gallery/RESTheart/wiki)

[Using API by Examples](https://github.com/docker-gallery/RESTheart/wiki/API-by-Examples)

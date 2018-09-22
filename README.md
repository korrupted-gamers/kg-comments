## wonderfall/isso

![](https://i.goopics.net/q1.png)


#### What is this?
Isso is a commenting server similar to Disqus. More info on the [official website](https://posativ.org/isso/).

#### Features
- Based on Alpine Linux 3.3.
- Latest Isso installed with `pip`.

#### Build-time variables
- **ISSO_VER** : version of Isso.

#### Environment variables
- **GID** : isso group id *(default : 991)*
- **UID** : isso user id *(default : 991)*

#### Volumes
- **/config** : location of configuration files.
- **/db** : location of SQLite database.

#### Ports
- **8080** [(reverse proxy!)](https://github.com/hardware/mailserver/wiki/Reverse-proxy-configuration).

#### KG Clan deployment
Here is the full documentation : https://posativ.org/isso/docs/

Used with dokku. First on the dokku host, add an isso app

    dokku apps:create isso

Create a config file on the dokku host. I put mine in /root/isso-cfg/isso.conf

```
[general]
dbpath = /db/comments.db
host =
  http://kgclan.club
  http://www.kgclan.club
  http://korruptedgamers.com
  http://www.korruptedgamers.com

[server]
listen = http://0.0.0.0:8080/
```


Create a Dokku storage volume for the config file and the database sqlite file

    dokku storage:mount isso /root/isso-cfg:/config
    dokku storage:mount isso /root/isso-db:/db

Push this repo to Dokku

    git push dokku master

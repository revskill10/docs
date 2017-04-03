# Dokku at Enrian

## [Dokku docs](http://dokku.viewdocs.io/dokku)
## [kk.enrian.com](http://kk.enrian.com)
### Jindrich Skupa

---

# What is Dokku ?

* The smallest PaaS implementation you've ever seen
* Dokku is an extensible, open source Platform as a Service that runs on a single server of your choice
* Heroku on our own
* Docker based application hosting
* `100 lines bash script` (currently not true)
* Extensible, Customizable

---

# Dokku

* deploy application with `git push dokku master`
  * ruby, java, nodejs, ...
  * docker container
* configure services
  * RDBMS databases (MySQL, PostgreSQL)
  * NoSQL databases (ElasticSearch, MongoDB)
  * Key-value databases (Memcached, Redis)
* automatic nginx vhost management

---

# Application management

## list existing apps
```
ssh dokku@enrian-kk apps
=====> My Apps
ruby-rails-sample
```

## create new app
```
ssh dokku@enrian-kk apps:create nodejs-example
Creating nodejs-example... done
```

## remove existing app
```
ssh dokku@enrian-kk apps:destroy ruby-rails-sample
 !     WARNING: Potentially Destructive Action
```

---

# Services management

## create redis for new app
```
ssh dokku@enrian-kk redis:create nodejs-example
       Waiting for container to be ready
=====> Redis container created: nodejs-example
=====> Container Information
       Config dir:  /var/lib/dokku/services/redis/nodejs-example/config
       Data dir:    /var/lib/dokku/services/redis/nodejs-example/data
       Dsn:         redis://nodejs-example:bf05fa0739329dfd56346e53aae6b3e3051b69da345657e256bbe0f11cd3738a@dokku-redis-nodejs-example:6379
```
## list services
```
ssh dokku@enrian-kk redis:list
NAME            VERSION      STATUS   EXPOSED PORTS  LINKS
nodejs-example  redis:3.2.3  running  -              nodejs-example
```

---

# Links services to application

## link redis to app
```
ssh dokku@enrian-kk redis:link nodejs-example nodejs-example
no config vars for nodejs-example
-----> Setting config vars
       REDIS_URL: redis://nodejs-example:bf05fa0739329dfd56346e53aae6b3e3051b69da345657e256bbe0f11cd3738a@dokku-redis-nodejs-example:6379
-----> Restarting app nodejs-example
App nodejs-example has not been deployed
```

---

# Application deployment

## git push dokku master
```
git remote add dokku dokku@enrian-kk:nodejs-example
git push dokku master

git push dokku master
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (6/6), 1.39 KiB | 0 bytes/s, done.
Total 6 (delta 0), reused 0 (delta 0)
-----> Cleaning up...
-----> Building nodejs-example from herokuish...
-----> Adding BUILD_ENV to build environment...
-----> Node.js app detected

-----> Creating runtime environment
...
=====> Application deployed:
       http://nodejs-example.kk.enrian.com
```

---

# Application management

## ps
```
ssh dokku@enrian-kk ps:stop nodejs-example
ssh dokku@enrian-kk ps:start nodejs-example
ssh dokku@enrian-kk ps:restart nodejs-example
ssh dokku@enrian-kk ps:rebuild nodejs-example
```

## get logs
```
ssh dokku@enrian-kk logs nodejs-example
```

## disable zero downtime checks
```
ssh dokku@enrian-kk checks:disable nodejs-example
-----> Disabling zero downtime for app (nodejs-example)
```

---

# Scale and proxy

## scale application
```
ssh dokku@enrian-kk ps:scale nodejs-example web=2
```

## port mappings
```
ssh dokku@enrian-kk proxy:ports nodejs-example
-----> Port mappings for nodejs-example
-----> scheme       host port        container port
http                80               5000
```

---

# User management

## list users
```
ssh dokku@enrian-kk ssh-keys:list
e4:d1:..:41:76 NAME="admin" SSHCOMMAND_ALLOWED_KEYS="no-agent-forwarding,no-user-rc,no-X11-forwarding,no-port-forwarding"
0d:91:..:a0:0e NAME="cervajz" SSHCOMMAND_ALLOWED_KEYS="no-agent-forwarding,no-user-rc,no-X11-forwarding,no-port-forwarding"
17:0b:..:34:a8 NAME="papricek" SSHCOMMAND_ALLOWED_KEYS="no-agent-forwarding,no-user-rc,no-X11-forwarding,no-port-forwarding"
84:54:..:b3:65 NAME="adam" SSHCOMMAND_ALLOWED_KEYS="no-agent-forwarding,no-user-rc,no-X11-forwarding,no-port-forwarding"
03:fc:..:32:90 NAME="pavel" SSHCOMMAND_ALLOWED_KEYS="no-agent-forwarding,no-user-rc,no-X11-forwarding,no-port-forwarding"
14:3a:..:71:e7 NAME="choke" SSHCOMMAND_ALLOWED_KEYS="no-agent-forwarding,no-user-rc,no-X11-forwarding,no-port-forwarding"
```
## add user
```
cat key.pub | ssh dokku@enrian-kk ssh-keys:add john_doe
```

---

# Q & A

## Thank you ...
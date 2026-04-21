---
title: Connecting Locally Installed Rails 5 To A Dockerised Postgres 12
description: There is a lot of information how to dockerise a rails app and a database, but not a lot of help to only dockerise the database. Here's how.
layout: post
categories: [docker, programming]
---
Here's how I managed to get my database dockerised without dockerising my Rails app. There’s a ton of information out there about how to dockerise both but I struggled to find much help on how to put only the database in Docker.

I was previously running Postgres via Homebrew and encountered several problems:

- It’s difficult to swap between database versions between applications
- Once I accidentally ran brew upgrade without pinning the version, and bumped the major version of postgres

I didn’t want to dockerise both because I want to be able to debug Rails in RubyMine and I haven’t found a way to do this yet.

## HOW TO
Install ‘postgresql’ with Brew, not postgresql@12 or any other pinned version, the pg gem for Rails needs it because it installs libpq which it needs to build successfully (you’ll get bundler errors otherwise).

Make sure the exposed port for postgres is 5432:5432 in the dockerfile (this is the default port Postgres 12 runs on).

In Rails, use the default user & password OR make a new one in Postgres then add the credentials to your database.yml file under both ‘development’ and ‘test’.

```yaml
username: postgres
password: 'mypasswordhere'
host: localhost
```

define the password in docker-compose.yml file
```yaml
environment:
POSTGRES_PASSWORD: "mypasswordhere"
```
Sample [docker-compose.yml](https://gist.github.com/outragedpinkracoon/300f74fb6232b4893b5db988f8e0dfb1)

## BONUS: RESTORE THE DATABASE FROM HEROKU
heroku pg:backups:capture
heroku pg:backups:download

User is superuser postgres unless you have set up another role.

```bash
pg_restore --verbose --clean --no-acl -U postgres --no-owner -h localhost -d my_database_name latest.dump
```

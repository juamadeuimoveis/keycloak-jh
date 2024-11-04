# Deploy Keycloak.X to Heroku

This repository deploys the [Keycloak.X](https://www.keycloak.org) Identity and Access Management Solution
to Heroku.  It is based of Keycloak's official docker image with some slight modifications to use the
Heroku variable for `PORT` and `DATABASE_URL` properly, also enabling the [edge](https://github.com/keycloak/keycloak-community/blob/main/design/keycloak.x/configuration.md#proxy-mode) 
proxy mode by default.

Keycloak.X uses Quarkus as the platform to build Keycloak. Compared to WildFly this gives faster startup-time 
and lower memory footprint which makes it possible for us to use a `free` dyno instance together with a `hobby-dev` 
Postgres database attached.

You only need to have a Heroku (free) account and everything will be sorted out with a click of a button via the web console :)

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

### Manual Deployment (Optional)
If you **don't want to use** the `Deploy to Heroku` button above for any reason, you need the Heroku CLI installed, so you can deploy this manually in a few steps after cloning this repository:
```shell
heroku apps:create --manifest
heroku addons:create heroku-postgresql:hobby-dev
heroku stack:set container
git push heroku main
```

### Known Issues
- In some cases, Heroku stops the service startup because it becomes unresponsive given the latency of the automatic database migration execution in the first initialization. If that happens, you can request for [changing the boot timeout](https://tools.heroku.support/limits/boot_timeout) manually for you app.

## References
- [Keycloak.X Docker Image](https://github.com/keycloak/keycloak-containers/tree/main/server-x)
- [Keycloak.X Server Configuration](https://github.com/keycloak/keycloak-community/blob/main/design/keycloak.x/configuration.md)
- [Introducing Keycloak.X Distribution](https://www.keycloak.org/2020/12/first-keycloak-x-release.adoc)
- [Deploy Keycloak to Heroku (Wildfly)](https://github.com/mieckert/keycloak-heroku)

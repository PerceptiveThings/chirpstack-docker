# chirpstack-docker Configuration

## Environment Variables

* POSTGRESQL_DSN: Full DSN of the postgresql instance (optional)
* CHIRPSTACK_HOST: hostname of chirpstack instance
* API_HOST: hostname of chirpstack REST api endpoint
* DEFAULT_EMAIL: email address to use for Let's Encrypt notices (optional)

## Let's Encrypt

This `docker compose` configuration is set up to use nginx and Let's Encrypt to securely proxy to Chirpstack. It is configured to have different hostnames for the main Chirpstack application and the REST API.

Make sure that DNS entries for `CHIRPSTACK_HOST` and `API_HOST` are set up before launching as the Let's Encrypt certificate creation will fail if it is not properly set up. If there are too many failures there will be a backoff period (an hour or more) before it can be attempted again.

## Launching with postgres

By default, this configuration will not spin up a postgresql environment, as we do not need one when running in production. If you want postgresql to be running you must include the `postgres` profile in the `docker compose` command:

```sh
$ docker compose --profile postgres up
$ COMPOSE_PROFILES=postgres docker compose up
```

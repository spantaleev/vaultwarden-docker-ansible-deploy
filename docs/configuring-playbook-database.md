# Configuring the database

By default, this playbook installs Postgres in a container alongside Vaultwarden.

To use your own Postgres server, use a `vars.yml` configuration like this:

```yaml
# Disable the integrated Postgres service
devture_postgres_enabled: false

# Uncomment and possibly change this, if you'd like to use another database engine.
# devture_vaultwarden_database_type: mysql

# Fill these out
devture_vaultwarden_database_hostname: ''
devture_vaultwarden_database_port: 5432
devture_vaultwarden_database_name: ''
devture_vaultwarden_database_username: ''
devture_vaultwarden_database_password: ''

# Alternatively, just set `devture_vaultwarden_config_database_url`
# to influence the `DATABASE_URL` environment variable passed to Vaultwarden.
```

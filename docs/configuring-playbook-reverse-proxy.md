# Configuring the reverse-proxy

By default, this playbook installs a [Traefik](https://traefik.io/) reverse-proxy, but that can be disabled if you'd like to using your own Traefik instance or to reverse-proxy in another way.


## Reverse-proxy type

To control the playbook's reverse-proxy integration use `devture_vaultwarden_playbook_reverse_proxy_type` variable, which controls the type of reverse-proxy that the playbook will use. Valid values:

  - `playbook-managed-traefik` (the default)
  - `other-traefik-container`
  - `none`

Learn more about these values and their behavior from [roles/custom/devture_vaultwarden_playbook_base/defaults/main.yml](../roles/custom/devture_vaultwarden_playbook_base/defaults/main.yml)


## Other variables of interest

The variables below are **automatically set** based on the reverse-proxy type (`devture_vaultwarden_playbook_reverse_proxy_type`). Nevertheless, you may find them useful if you need to do something more advanced.

- `devture_traefik_enabled` (same as `devture_vaultwarden_playbook_traefik_role_enabled` by default - `true`) - controls whether the Traefik role's functionality is enabled or not. If disabled, the role will try to uninstall Traefik, etc. Flipping this to `false` disables Traefik, but also potentially uninstalls and deletes data in `/devture-traefik`.

- `devture_vaultwarden_playbook_traefik_role_enabled` (default `true`) - controls whether the Traefik role will execute or not. Setting this to `false` disables Traefik and doesn't touch `/devture-traefik` (which is potentially managed by another playbook)

- `devture_vaultwarden_playbook_traefik_labels_enabled` (default `true`) - controls whether Traefik container labels are attached to services. You may disable Traefik with the variables above, yet still keep attaching labels, so that a separately-installed Traefik instance can reverse-proxy to these services. If you're not using Traefik at all, flip this to `false`

- `devture_vaultwarden_playbook_reverse_proxyable_services_additional_network` (default `traefik`) - additional container network for reverse-proxyable services (like `vaultwarden`). We default these to the `traefik` network for the default Traefik installation's benefit, but you can set this to another network


## Examples

### Using Traefik in local-only mode

Below is an example of **putting Traefik in local-only mode** (no SSL termination) and letting you use another SSL-terminating reverse-proxy in front:

```yaml
# We keep the default reverse-proxy type
# devture_vaultwarden_playbook_reverse_proxy_type: playbook-managed-traefik

# We disable Traefik's web-secure endpoint, which will disable SSL certificate retrieval and http-to-https redirection
devture_traefik_config_entrypoint_web_secure_enabled: false
```

You can now reverse-proxy to port `80` where Traefik handles domains for all services managed by the playbook (Vaultwarden and potentially others, if enabled).


### Disabling Traefik and reverse-proxying manually

Below is an example of **disabling Traefik completely** and letting you reverse-proxy using other means:

```yaml
devture_vaultwarden_playbook_reverse_proxy_type: none

# Expose the Vaultwarden container's webserver to port 8080 on the loopback network interface only.
# You can reverse-proxy to it using a locally running webserver.
devture_vaultwarden_container_http_bind_port: '127.0.0.1:8080'

# Or:
# Expose the Vaultwarden container's webserver to port 8080 on all network interfaces.
# You can reverse-proxy to it from another machine on the public or private network.
# devture_vaultwarden_container_http_bind_port: '8080'
```

You can now reverse-proxy to port `8080` for Vaultwarden. If you need to expose other services managed by this playbook, you'd need to expose them the same way (`_bind_port` variables) manually.

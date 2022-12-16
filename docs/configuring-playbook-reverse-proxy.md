# Configuring the reverse-proxy

By default, this playbook installs a [Traefik](https://traefik.io/) reverse-proxy, but that can be disabled if you'd like to using your own Traefik instance or to reverse-proxy in another way.

There are multiple variables in the playbook which control Traefik integration:

- `devture_traefik_enabled` (same as `devture_vaultwarden_playbook_traefik_role_enabled` by default - `true`) - controls whether the Traefik role's functionality is enabled or not. If disabled, the role will try to uninstall Traefik, etc. Flipping this to `false` disables Traefik, but also potentially uninstalls and deletes data in `/devture-traefik`.

- `devture_vaultwarden_playbook_traefik_role_enabled` (default `true`) - controls whether the Traefik role will execute or not. Setting this to `false` disables Traefik and doesn't touch `/devture-traefik` (which is potentially managed by another playbook)

- `devture_vaultwarden_playbook_traefik_labels_enabled` (default `true`) - controls whether Traefik container labels are attached to services. You may disable Traefik with the variables above, yet still keep attaching labels, so that a separately-installed Traefik instance can reverse-proxy to these services. If you're not using Traefik at all, flip this to `false`

- `devture_vaultwarden_playbook_reverse_proxyable_services_additional_network` (default `traefik`) - additional container network for reverse-proxyable services (like `vaultwarden`). We default these to the `traefik` network for the default Traefik installation's benefit, but you can set this to another network

Below is an example of **disabling Traefik completely** and letting you reverse-proxy using other means:

```yaml
# Disable the Traefik role completely
devture_vaultwarden_playbook_traefik_role_enabled: false

# If you're not using Traefik, disable putting Traefik labels on services
devture_vaultwarden_playbook_traefik_labels_enabled: false

# Expose the Vaultwarden container's webserver to port 8080 on the loopback network interface only.
# You can reverse-proxy to it using a locally running webserver.
devture_vaultwarden_container_http_bind_port: '127.0.0.1:8080'

# Or:
# Expose the Vaultwarden container's webserver to port 8080 on all network interfaces.
# You can reverse-proxy to it from another machine on the public or private network.
# devture_vaultwarden_container_http_bind_port: '8080'
```

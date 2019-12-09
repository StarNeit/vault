---
layout: "docs"
page_title: "Service Registration - Configuration"
sidebar_title: "<code>service_registration</code>"
sidebar_current: "docs-configuration-serviceDiscovery"
description: |-
  The optional `service_registration` stanza configures Vault's mechanism for
  service registration.  
---

# `service_registration` Stanza

The optional `service_registration` stanza configures Vault's mechanism for
service registration.  The `service_registration` stanza is designed for use cases
where you would like to use a system like [Consul][consul] for [service
discovery][consul-discovery], but use a different system for the [storage
backend][storage-backend].  

When Consul is configured as the [storage backend][consul-backend], Vault
implicitly uses Consul for service registration, so the `service_registration` stanza
is not needed.  

For times when you would like to use a different storage backend, like
[Raft][raft-backend], but still have service registration available, the
`service_registration` stanza can be used:

```hcl
service_registration "consul" {
  address = "127.0.0.1:8500"
}
storage "raft" {
  path = "/path/to/raft/data"
  node_id = "raft_node_1"
}
```

For information about a specific service registration provider, choose one from
the navigation on the left.

## Configuration

Service registration configuration is done through the Vault configuration file
using the `service_registration` stanza:

```hcl
service_registration [NAME] {
  [PARAMETERS...]
}
```

For example:

```hcl
service_registration "consul" {
  address = "127.0.0.1:8500"
}
```

For configuration options which also read an environment variable, the
environment variable will take precedence over values in the configuration
file.

[consul]: https://www.consul.io/
[consul-discovery]: https://www.consul.io/discovery.html
[storage-backend]: /docs/configuration/storage/index.html
[consul-backend]: /docs/configuration/storage/consul.html
[raft-backend]: /docs/configuration/storage/raft.html
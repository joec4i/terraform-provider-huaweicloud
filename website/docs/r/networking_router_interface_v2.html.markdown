---
layout: "huaweicloud"
page_title: "HuaweiCloud: huaweicloud_networking_router_interface_v2"
sidebar_current: "docs-huaweicloud-resource-networking-router-interface-v2"
description: |-
  Manages a V2 router interface resource within HuaweiCloud.
---

# huaweicloud\_networking\_router_interface_v2

Manages a V2 router interface resource within HuaweiCloud.

## Example Usage

```hcl
resource "huaweicloud_networking_network_v2" "network_1" {
  name           = "tf_test_network"
  admin_state_up = "true"
}

resource "huaweicloud_networking_subnet_v2" "subnet_1" {
  network_id = "${huaweicloud_networking_network_v2.network_1.id}"
  cidr       = "192.168.199.0/24"
  ip_version = 4
}

resource "huaweicloud_networking_router_v2" "router_1" {
  name                = "my_router"
  external_network_id = "f67f0d72-0ddf-11e4-9d95-e1f29f417e2f"
}

resource "huaweicloud_networking_router_interface_v2" "router_interface_1" {
  router_id = "${huaweicloud_networking_router_v2.router_1.id}"
  subnet_id = "${huaweicloud_networking_subnet_v2.subnet_1.id}"
}
```

## Argument Reference

The following arguments are supported:

* `region` - (Optional) The region in which to obtain the V2 networking client.
    A networking client is needed to create a router. If omitted, the
    `region` argument of the provider is used. Changing this creates a new
    router interface.

* `router_id` - (Required) ID of the router this interface belongs to. Changing
    this creates a new router interface.

* `subnet_id` - ID of the subnet this interface connects to. Changing
    this creates a new router interface.

* `port_id` - ID of the port this interface connects to. Changing
    this creates a new router interface.

## Attributes Reference

The following attributes are exported:

* `region` - See Argument Reference above.
* `router_id` - See Argument Reference above.
* `subnet_id` - See Argument Reference above.
* `port_id` - See Argument Reference above.

## Import

Router Interfaces can be imported using the port `id`, e.g.

```
$ openstack port list --router <router name or id>
$ terraform import huaweicloud_networking_router_interface_v2.int_1 <port id from above output>
```

# Azure virtual network module

## Example of `vnet_subnet_range`

```terraform
vnet_subnet_range = {
  # Subnet without service_delegation
  "backend-snet" = {
    "ip_range"                                      = "10.10.98.0/24"
    "attach_nsg"                                    = true
    "attach_route_table"                            = false
    "service_endpoints"                             = []
    "private_endpoint_network_policies_enabled"     = true
    "private_link_service_network_policies_enabled" = true
    "service_delegation"                            = null
    "service_delegation_actions"                    = []
  }
  # Subnet with service_delegation
  "databricks-snet" = {
    "ip_range"                                      = "10.10.99.0/24"
    "attach_nsg"                                    = true
    "attach_route_table"                            = false
    "service_endpoints"                             = ["Microsoft.Storage", "Microsoft.Sql", "Microsoft.KeyVault"]
    "private_endpoint_network_policies_enabled"     = true
    "private_link_service_network_policies_enabled" = true
    "service_delegation"                            = "Microsoft.Databricks/workspaces",
    "service_delegation_actions"                    = ["Microsoft.Network/virtualNetworks/subnets/join/action", "Microsoft.Network/virtualNetworks/subnets/prepareNetworkPolicies/action", "Microsoft.Network/virtualNetworks/subnets/unprepareNetworkPolicies/action", ]
  }
}
```

## Bastion

If you populate `bastion_subnet_range` a Bastion host will be deployed in the VNET resource group.

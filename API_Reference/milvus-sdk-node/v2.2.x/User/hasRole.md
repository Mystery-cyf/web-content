# hasRole()

This method checks if the role is existing.

```javascript
new milvusClient(MILUVS_ADDRESS).userManager.hasRole(HasRoleReq);
```

### HasRoleReq

| Parameters | Description                                                                            | Type   |
| ---------- | -------------------------------------------------------------------------------------- | ------ |
| roleName   | The role name                                                                          | String |
| timeout?   | This parameter is used to specify the length of time, in milliseconds, that the RPC (Remote Procedure Call) is allowed to run. If no value is provided, the default is undefined. | Number |

## Example

```javascript
import { MilvusClient } from "@zilliz/milvus2-sdk-node";

new milvusClient(MILUVS_ADDRESS).userManager.hasRole({
  roleName: "my-role",
});
```

### Response
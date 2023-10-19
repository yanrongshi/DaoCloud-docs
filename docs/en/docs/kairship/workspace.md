# Workspaces

Workspaces are a hierarchical mapping of resources designed for managing global resources in DCE 5.0. A workspace can be understood as a project within a department, and administrators map the relationship between departments and projects using folders and workspaces. For more detailed information about workspaces, refer to the [Workspace and Hierarchy](../ghippo/user-guide/workspace/workspace.md) documentation.

## Considerations

- The current operating user should have Admin or Workspace Admin permissions. For more information on permissions, refer to the [Role and Permission Management](../ghippo/user-guide/access-control/role.md) and [Workspace Permissions](../ghippo/user-guide/workspace/ws-permission.md) documentation.
- After binding a multi-cloud instance/namespace with a workspace, all working clusters under the multi-cloud instance will automatically synchronize this binding, allowing users of the corresponding workspace to operate corresponding resources in the cluster.
- After binding, you can go to the `Workspace & Hierarchy` -> `Resource Group` section in the Global Management module to view this resource. For more details, refer to the [Resource Quota](../ghippo/user-guide/workspace/quota.md#_1) documentation.
- Currently, one multi-cloud instance/namespace can only be bound to one workspace, creating a one-to-one mapping relationship.

    - This ensures stable matching of resources and permissions, preventing resource and permission conflicts.
    - In the future, we will support binding a multi-cloud instance or namespace as a shared resource to multiple workspaces. This feature is currently under development, so stay tuned.

## Bind/Unbind Workspace

In the Multicloud Management module, admin of the DCE 5.0 platform can bind multicloud instances or multicloud namespaces to a workspace.

After the binding, users of that workspace can operate instances or namespaces within their permission scope.

1. Click `Workspace` in the upper-right corner of the homepage of the Multicloud Management module.

    ![Management entrance.png](https://docs.daocloud.io/daocloud-docs-images/docs/en/docs/kairship/images/ws01.png)

2. Check the binding status of multicloud instances/namespaces, then click the `ⵗ` action button and select `Bind Workspace` or `Unbind Workspace` as needed.

    ![Management interface](https://docs.daocloud.io/daocloud-docs-images/docs/en/docs/kairship/images/ws02.png)

3. Select which workspace to bind when binding, or just confirm your action when unbinding.

    ![Binding/Unbinding](https://docs.daocloud.io/daocloud-docs-images/docs/en/docs/kairship/images/ws03.png)

    ![Binding/Unbinding](https://docs.daocloud.io/daocloud-docs-images/docs/en/docs/kairship/images/ws04.png)

!!! note

    - After multicloud instances/namespaces are bound to a workspace, all working clusters under the multicloud instance will automatically synchronize this binding relationship, allowing users in that workspace to operate the corresponding resources in the cluster.
    - After the binding, you can enter the `Workspace and Folder` -> `Resource Group` section of the DCE 5.0 Global Management module to view the resources. For more details, see [Resource Quotas](../ghippo/user-guide/workspace/quota.md#_1).
    - Currently, one multicloud instance/namespace can be bound to ONLY ONE workspace. The mapping relationship is one-to-one.

        - This ensures stable matching of resources and permissions, preventing resource and permission conflicts.
        - In the future, the multicloud instance or namespace can be bound to multiple workspaces as shared resources. This feature is currently under development, stay tuned.

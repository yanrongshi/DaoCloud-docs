---
hide:
  - toc
---

# Creating/Deleting Folders

Folders have the capability to map permissions, allowing users/user groups to have their permissions in the folder mapped to its sub-folders, workspaces, and resources.

Follow the steps below to create a folder:

1. Log in to DCE 5.0 with a user account having the admin/folder admin role.
   Click `Global Management` -> `Workspace and Folder` at the bottom of the left navigation bar.

    ![Global Management](../../images/ws01.png)

2. Click the `Create Folder` button in the top right corner.

    ![Create Folder](../../images/ws02.png)

3. Fill in the folder name, parent folder, and other information, then click `OK` to complete creating the folder.

    ![Confirm](../../images/fd03.png)

!!! tip

    After successful creation, the folder name will be displayed in the left tree structure, represented by different icons for workspaces and folders.

    ![Workspaces and Folders](../../images/fd04.png)

!!! note

    To edit or delete a specific folder, select it and Click `...` on the right side.

    - If there are resources bound to the resource group or shared resources within the folder, the folder cannot be deleted. All resources need to be unbound before deleting.

    - If there are registry resources accessed by the microservice engine module within the folder, the folder cannot be deleted. All access to the registry needs to be removed before deleting the folder.

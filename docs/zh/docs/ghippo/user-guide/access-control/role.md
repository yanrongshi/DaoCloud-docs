# 角色和权限管理

一个角色对应一组权限。权限决定了可以对资源执行的操作。向用户授予某角色，即授予该角色所包含的所有权限。
  
DaoCloud Enterprise 5.0 平台存在三种角色范围，能够灵活、有效地解决您在权限上的使用问题：
  
- [平台角色](#_2)
- [工作空间角色](#_4)
- [文件夹角色](#_6)
  
## 平台角色
  
平台角色是粗粒度权限，对平台上所有相关资源具有相应权限。通过平台角色可以赋予用户对所有集群、所有工作空间等的增删改查权限，而不能具体到某一个集群或某一个工作空间。DaoCloud Enterprise 5.0 提供了 5 个预置的平台角色，分别是 Admin / Kpanda Owner / Workspace and Folder Owner / IAM Owner / Audit Owner，用户可直接使用。

![三种权限模式](https://huatu.98youxi.com/markdown/work/uploads/upload_b112ad9ac722b753f7fb5e62266a4614.png)

同时，DaoCloud Enterprise 5.0 还支持用户创建自定义平台角色，可根据需要自定义角色内容。如创建一个平台角色，包含应用工作台的所有功能权限，由于应用工作台依赖于工作空间，因此平台会帮助用户默认勾选工作空间的查看权限，请不要手动取消勾选。若用户 A 被授予该 workbench 角色，将自动拥有所有工作空间下的应用工作台相关功能的增删改查等权限。

![](https://huatu.98youxi.com/markdown/work/uploads/upload_11ee0542ab53f2633f865c66852252eb.png)


### 平台角色授权方式

方式一：在`全局管理` -> `用户与访问控制` -> `用户`的用户列表中，找到该用户，单击 `...`，选择`授权`，为该用户赋予平台角色权限。
![](https://huatu.98youxi.com/markdown/work/uploads/upload_fb27d37995508fd3b1f25f4e46af8cc5.png)
  
方式二：在`全局管理` -> `用户与访问控制` -> `用户组`的用户组列表中创建用户组，将该用户加入用户组，并给用户组授权（具体操作为：在用户组列表找到该用户组，单击 `...`，选择`授权`，为该用户组赋予平台角色）。
![](https://huatu.98youxi.com/markdown/work/uploads/upload_b00e8064dced431f568d347b779ec9e9.png)

方式三：在`全局管理` -> `用户与访问控制` -> `角色`的角色列表中，找到相应的平台角色，单击角色名称进入详情，单击`关联用户` 按钮，选中该用户或用户所在的用户组，单击`确定`。
![](https://huatu.98youxi.com/markdown/work/uploads/upload_30dfc3fbb5c8f13a9b2d6d2ef4e40849.png)

## 工作空间角色
  
工作空间角色是细粒度角色，通过工作空间角色可以赋予用户某个工作空间的管理权限、查看权限或该工作空间应用工作台相关的权限等。获得该角色权限的用户只能管理该工作空间，而无法访问其他工作空间。 DaoCloud Enterprise 5.0 提供了 3 个预置的工作空间角色，分别是 Workspace Admin / Workspace Editor / Workspace Viewer 用户可直接使用。
![](https://huatu.98youxi.com/markdown/work/uploads/upload_091ce2649f460fcefb19510f2dbf2011.png)

同时，DaoCloud Enterprise 5.0 还支持用户创建自定义工作空间角色，可根据需要自定义角色内容。如创建一个工作空间角色，包含应用工作台的所有功能权限，由于应用工作台依赖于工作空间，因此平台会帮助用户默认勾选工作空间的查看权限，请不要手动取消勾选。若用户 A 在工作空间 01 中被授予该角色，将拥有工作空间 01 下的应用工作台相关功能的增删改查权限。

!!! note
  
    与平台角色不同，工作空间角色被创建后需要前往工作空间使用，被授权后用户仅在该工作空间下拥有该角色中的功能权限。

### 工作空间角色授权方式

在`全局管理` -> `工作空间与层级` 列表中，找到该工作空间，点击 `添加授权`，为该用户赋予工作空间角色权限。
![](https://huatu.98youxi.com/markdown/work/uploads/upload_045f72bb3c813b7855b9c305a3c3ea61.png)
![](https://huatu.98youxi.com/markdown/work/uploads/upload_5cf1f6ee159ed4b0df705d3427ee9fb6.png)
  
## 文件夹角色

文件夹角色的权限粒度介于平台角色与工作空间角色之间，通过文件夹角色可以赋予用户某个文件夹及其子文件夹和该文件夹下所有工作空间的管理权限、查看权限等，常适用于企业中的部门场景。比如用户 B 是一级部门的 Leader ，通常用户 B 能够管理该一级部门、其下的所有二级部门和部门中的项目等，在此场景中给用户 B 授予一级文件夹的管理员权限，用户 B 也将拥有其下的二级文件夹和工作空间的相应权限。DaoCloud Enterprise 5.0 提供了 3 个预置的文件夹角色，分别是 Folder Admin / Folder Editor / Folder Viewer，用户可直接使用。
![](https://huatu.98youxi.com/markdown/work/uploads/upload_6c7f103f57a3cfa5ebbcf8343eba8075.png)

同时，DaoCloud Enterprise 5.0 还支持用户创建自定义文件夹角色，可根据需要自定义角色内容。如创建一个文件夹角色，包含应用工作台的所有功能权限。若用户 A 在文件夹 01 中被授予该角色，将拥有该文件夹下所有工作空间中应用工作台相关功能的增删改查权限。

!!! note
  
    功能模块本身依赖的是工作空间，文件夹是工作空间上的进一步分组机制且具有权限继承能力，因此文件夹权限不光包含文件夹本身，还包括其下的子文件夹和工作空间。

### 文件夹角色授权方式

在`全局管理` -> `工作空间与层级` 列表中，找到该文件夹，单击 `添加授权`，为该用户赋予文件夹角色权限。
![](https://huatu.98youxi.com/markdown/work/uploads/upload_5c1258b94bb7e5a6338590d9455d6b84.png)
![](https://huatu.98youxi.com/markdown/work/uploads/upload_07ac128ed492212669887aa04febe567.png)


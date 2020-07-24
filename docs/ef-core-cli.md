# ef-core

## ef-core 安装

```shell

dotnet tool  install --global dotnet-ef

```

## ef-core 迁移数据

```shell
#创建迁移
dotnet ef migrations add migrationname
#指定dbcontext创建迁移
dotnet ef migrations add migrationname --context dbcontext

#删除迁移
dotnet ef migrations remove

#应用迁移/指定迁移
dotnet ef database update
dotnet ef database update migrationname

#查看所有迁移
dotnet ef migrations list

```

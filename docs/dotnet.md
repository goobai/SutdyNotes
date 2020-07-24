#dotnet 命令行

## 

```shell script
dotnet restore .\V2Mall.Web.csproj
dotnet build .\V2Mall.Web.csproj -c release -o ./build

consul.exe agent -dev
```

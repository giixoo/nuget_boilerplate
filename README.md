# nuget boilerplate
boilerplate for nuget package project

Follow this steps to create your own:

### 1. Create new dot net console application from UI or from command line

```bash
dotnet new console -n my-awesome-project
```

### 2. Update csproj file
To build project as nuget tool package add 
```xml
        <PackAsTool>true</PackAsTool>
        <ToolCommandName>my-awesome-tool</ToolCommandName>
        <PackageOutputPath>.nupkg</PackageOutputPath>
```
to your `.scproj` file 

### 3. Create Nuget package
In the project folder run
```bash
dotnet pack 
```

To create the release version, run
```bash
dotnet pack -c Release
```

### 4. Install from the local build
Run the following command:
```bash
dotnet tool install -g --add-source .\.nupkg\ my-awesome-project
```

where
- `-g` options stands for global tool installation
- `--add-source <folder name with nuget>` required only for installing local nuget package
- `my-awesome-project` is root namespace of the project

Check installed tools with 
```bash
dotnet tool list -g
```

Uninstall tool by running
```bash
dotnet tool uninstall my-awesome-project -g
```

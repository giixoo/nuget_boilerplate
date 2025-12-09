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
### 5. Upload package to NuGet

To upload our nuget package we have to register account on a nuget.org first, 
then confirm your email.
Login to your account and hit `Upload` button.
If you are lucky enough, you will not see 
```text
This package ID has been reserved. Please request access to upload to this reserved namespace from the owner of the reserved prefix, or re-upload the package with a different ID. Learn more about Package ID prefix reservation.
```
message, but in most cases do.
To fix it, you have to set *unique* name to your package.
Open your `.csproj` file and add following line:
```xml
	<PackageId>accountname.myawesometool</PackageId>
```
the prefix of package identifier should be unique across all packages, hence some effort required.

another error you may see is `License missing. See how to include a license within the package.` and 
`Readme missing. See how to include a readme file within the package, or add it as you upload.`

the first warning is about a missing license, 
we can add it by adding to the .csproj file another line
```xml
		<PackageLicenseExpression>MIT</PackageLicenseExpression>
```
I'm using an MIT license, but you can set a license that fits your needs better

missing readme file we can fix by adding the following in .csproj: 

```xml
    <PropertyGroup>
        ...
		<PackageReadmeFile>README.md</PackageReadmeFile>
        ...
    </PropertyGroup>

    <ItemGroup>
        <None Include="README.md" Pack="true" PackagePath="\"/>
    </ItemGroup>
```
and create the README.md file in the project folder

after rebuild upload process should go smoothly. 
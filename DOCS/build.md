# Building a .NetCore

## MsBuild

The csproj file is C# specific project file containing MSBuild XML.

Doing an analogy with Java, the csproj file is like pom.xml from Maven.

## Dependencies 

When you add a dependency to a project file, that dependency can be a package,
metapackage, or another project. A package is generally a NuGet package containing
files and assemblies organized by the framework those assemblies will work on. Meta-
packages reference a bunch of other packages and may also define a framework. An
example of a metapackage that defines a framework is the .NET Standard Library.


## Frameworks 

Frameworks, or more specifically target frameworks, are a NuGet concept.

To specify a framework, you need put the TargetFramework in your csproj file


```
<Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
        <TargetFramework>netstandard1.4</TargetFramework>
    </PropertyGroup>
</Project>
```


From the CLI, you would use the -f or --framework option to pick the target frame-
work you want to build, or test, or publish as follows:

```bash
dotnet build -f netcoreapp2.0
dotnet test -f netcoreapp2.0
```

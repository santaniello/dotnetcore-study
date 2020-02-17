# DOTNETCORE

Installation and configuration of the environment:
  - https://docs.microsoft.com/pt-br/dotnet/core/install/linux-package-manager-ubuntu-1904
  - https://medium.com/danielpadua/vscode-asp-net-core-preparar-ambiente-de-desenvolvimento-adf30cefea07

# Creating a new project

Consolle application:
```bash
dotnet new console
```
Template to create a minimal Web application:
```bash
dotnet new web
```

# Before you build

You now have the Hello World code and the project description, but there’s a critical
step that needs to take place before you build or run your application. You need to
restore your packages. You have a set of dependencies for your project, and each
dependency is a package that may also have its own dependencies. The package-
restore step expands the full tree of dependencies and determines which versions of
each package to install.

To do this, perform this command:

```bash
dotnet restore
```

Application Structure:

- Program.cs - Class that initializes the web server (Kestrel);
- Startup.cs - Used to define how the web requests will be treated. This class starts the web application.
- .csproj file - This file do a description about the our project (such as pom.xml in java);


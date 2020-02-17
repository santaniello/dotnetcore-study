# DOTNETCORE

Installation and configuration of the environment:
  - https://docs.microsoft.com/pt-br/dotnet/core/install/linux-package-manager-ubuntu-1904
  - https://medium.com/danielpadua/vscode-asp-net-core-preparar-ambiente-de-desenvolvimento-adf30cefea07

# Creating a new project

Consolle application:
```bash
dotnet new console
```
Web application:
```bash
dotnet new web
```

Application Structure:

- Program.cs - Class that initializes the web server (Kestrel);
- Startup.cs - Used to define how the web requests will be treated. This class starts the web application.
- .csproj file - This file do a description about the our project (such as pom.xml in java);


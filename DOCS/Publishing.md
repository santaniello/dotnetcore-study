# Publishing an application (framework-dependent deployment)

Execute the command below:

```bash
dotnet publish -c Release
```
The console output indicates to which folder the binaries are published.

There should be four files:

-  hwapp.deps.json
-  hwapp.dll
-  hwapp.pdb
-  hwapp.runtimeconfig.json

Copy these files to another machine that has the .NET Core SDK installed. Then, to
execute the application, run the command dotnet hwapp.dll from the folder con-
taining the copied files.

In this example, only the binaries built for the project, and any included packages,
are published. This is called a framework-dependent deployment. When you deploy the
files from the publish folder, you need to have the .NET Core SDK installed on the tar-
get machine.

To execute the application, just:

```bash
dotnet hwapp.dll
```

# Publishing a Self-Contained Application (You don't need to have the SDK installed)

To create a self-contained application, you’ll first need to be explicit about what
runtimes your application can run on. This is done by adding the Runtime-
Identifiers property to your project file, as shown in the following listing.


```xml
<Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
      <OutputType>Exe</OutputType>
      <TargetFramework>netcoreapp2.0</TargetFramework>
      <RuntimeIdentifiers>win10-x64;osx.10.11-x64;linuxmint.19.1-x64
      </RuntimeIdentifiers>
    </PropertyGroup>
</Project>
```

Now you can create a self-contained application by using the runtime identifier in the
publish command, as follows:


```bash
dotnet publish -c Release -r linuxmint.19.1-x64
```

To execute the application, just:

```bash
dotnet hwapp.dll
```

# Deploying to a Docker container

## Console Application

First, you need create a Dockerfile:


```
FROM mcr.microsoft.com/dotnet/core/sdk:3.1
COPY bin/Release/netcoreapp3.1/publish/ /root/
ENTRYPOINT dotnet /root/hwapp.dll
```

After, we need build the image:

```bash
docker build -t hwapp .
```

After, execute:

```bash
docker run -it hwapp
```

## Web Application

Firs, we need change de the Program class:

```c#
namespace hwwebapp
{
  public class Program
  {
    public static void Main(string[] args)
    {
       BuildWebHost(args).Run();
    }
    public static IWebHost BuildWebHost(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
           .UseUrls("http://*:5000/")  // add This Line
           .UseStartup<Startup>()            
           .Build();
  }
}
```

The added line allows URLs other than http://localhost:5000. Because the applica-
tion is being deployed to a container, you’ll need to test it by pinging it from outside
the container.

In the Dockerfile, we need expose the port to out of containter


```
FROM mcr.microsoft.com/dotnet/core/sdk:3.1
COPY bin/Release/netcoreapp3.1/publish/ /root/
EXPOSE 5000/tcp
ENTRYPOINT dotnet /root/hwwebapp.dll
```

And after:

```bash
dotnet publish -c Release
docker build -t hwwebapp .
docker run -it -p 5000:5000 hwwebapp
```

# Packaging for distribution


.NET Core makes it easy to package your library or application so that others can use
it in their applications.

To share your library with other applications, you need use the command:

```bash
dotnet pack -c Release
```

This command will create a hwapp.1.0.0.nupkg file

The .nupkg file produced by the dotnet pack command is a NuGet package.



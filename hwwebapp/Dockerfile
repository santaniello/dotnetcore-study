FROM  mcr.microsoft.com/dotnet/core/sdk:3.1
COPY bin/Release/netcoreapp3.1/publish/ /root/
EXPOSE 5000/tcp
ENTRYPOINT dotnet /root/hwwebapp.dll

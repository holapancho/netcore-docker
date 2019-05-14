FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY AnotherNetCoreDocker/AnotherNetCoreDocker.csproj AnotherNetCoreDocker/
RUN dotnet restore AnotherNetCoreDocker/AnotherNetCoreDocker.csproj
COPY . .
WORKDIR /src/AnotherNetCoreDocker
RUN dotnet build AnotherNetCoreDocker.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish AnotherNetCoreDocker.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AnotherNetCoreDocker.dll"]

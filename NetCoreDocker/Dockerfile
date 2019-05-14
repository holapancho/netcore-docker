FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY NetCoreDocker/NetCoreDocker.csproj NetCoreDocker/
RUN dotnet restore NetCoreDocker/NetCoreDocker.csproj
COPY . .
WORKDIR /src/NetCoreDocker
RUN dotnet build NetCoreDocker.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish NetCoreDocker.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "NetCoreDocker.dll"]

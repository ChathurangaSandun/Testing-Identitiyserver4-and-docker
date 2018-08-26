FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY src/Marvin.IDP/Marvin.IDP.csproj src/Marvin.IDP/
RUN dotnet restore src/Marvin.IDP/Marvin.IDP.csproj
COPY . .
WORKDIR /src/src/Marvin.IDP
RUN dotnet build Marvin.IDP.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Marvin.IDP.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Marvin.IDP.dll"]

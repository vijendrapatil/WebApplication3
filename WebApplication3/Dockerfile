FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 65391
EXPOSE 52153

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY WebApplication3/WebApplication3.csproj WebApplication3/
RUN dotnet restore WebApplication3/WebApplication3.csproj
COPY . .
WORKDIR /src/WebApplication3
RUN dotnet build WebApplication3.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish WebApplication3.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApplication3.dll"]

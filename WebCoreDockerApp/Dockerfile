FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-sac2016 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk-nanoserver-sac2016 AS build
WORKDIR /src
COPY ["WebCoreDockerApp/WebCoreDockerApp.csproj", "WebCoreDockerApp/"]
RUN dotnet restore "WebCoreDockerApp/WebCoreDockerApp.csproj"
COPY . .
WORKDIR "/src/WebCoreDockerApp"
RUN dotnet build "WebCoreDockerApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "WebCoreDockerApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebCoreDockerApp.dll"]
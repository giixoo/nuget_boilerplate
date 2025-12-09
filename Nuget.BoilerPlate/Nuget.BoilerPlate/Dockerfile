FROM mcr.microsoft.com/dotnet/runtime:9.0 AS base
USER $APP_UID
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["Nuget.BoilerPlate/Nuget.BoilerPlate.csproj", "Nuget.BoilerPlate/"]
RUN dotnet restore "Nuget.BoilerPlate/Nuget.BoilerPlate.csproj"
COPY . .
WORKDIR "/src/Nuget.BoilerPlate"
RUN dotnet build "./Nuget.BoilerPlate.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "./Nuget.BoilerPlate.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Nuget.BoilerPlate.dll"]

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src

# Copy everything
COPY MultiStage.csproj .
# Restore as distinct layers
RUN dotnet restore
COPY . .
# Build and publish a release
RUN dotnet build "MultiStage.csproj" -c Release -o /App/build

RUN dotnet publish -c Release -o /App

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:9.0
WORKDIR /App
COPY --from=build /App .
ENTRYPOINT ["dotnet", "MultiStage.dll"]
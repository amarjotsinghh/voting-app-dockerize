FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build

WORKDIR /source

# Copy everything before restoring to avoid missing references
COPY . ./

# Restore all dependencies
RUN dotnet restore

# Publish the application
RUN dotnet publish -c Release -o /app --self-contained false --no-restore

FROM mcr.microsoft.com/dotnet/runtime:7.0
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["dotnet", "Worker.dll"]

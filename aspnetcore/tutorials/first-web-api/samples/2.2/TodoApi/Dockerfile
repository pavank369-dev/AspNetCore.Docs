# Runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
WORKDIR /app
EXPOSE 80

# Build image
FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /src

# Copy everything and restore
COPY . .
RUN dotnet restore TodoApi.csproj

# Build and publish
RUN dotnet publish TodoApi.csproj -c Release -o /app/publish

# Final runtime image
FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .

# Entry point is the .dll built from the .csproj
ENTRYPOINT ["dotnet", "TodoApi.dll"]

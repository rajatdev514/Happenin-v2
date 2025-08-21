# Step 1: Use official .NET 9 SDK to build the app
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src

# Copy csproj and restore dependencies
COPY HappeninApi.csproj .
RUN dotnet restore HappeninApi.csproj

# Copy rest of the code and build
COPY . .
RUN dotnet publish HappeninApi.csproj -c Release -o /app/publish

# Step 2: Use .NET 9 runtime
FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish .

# Run app on port 10000
ENV ASPNETCORE_URLS=http://+:${PORT}
ENTRYPOINT ["dotnet", "HappeninApi.dll"]

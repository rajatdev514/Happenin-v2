# Step 1: Use official .NET SDK to build the app
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy csproj and restore dependencies
COPY HappeninApi.csproj .
RUN dotnet restore HappeninApi.csproj

# Copy rest of the code and build
COPY . .
RUN dotnet publish HappeninApi.csproj -c Release -o /app/publish

# Step 2: Use lightweight runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish .
EXPOSE 10000

# Run app on port 10000
ENV ASPNETCORE_URLS=http://+:10000
ENTRYPOINT ["dotnet", "HappeninApi.dll"]

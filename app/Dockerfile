# Stage 1: Build the C# App
# We use the full .NET SDK to build the code
FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
WORKDIR /src

# Copy the project file first (better caching)
COPY src/Api/Api.csproj ./src/Api/
RUN dotnet restore src/Api/Api.csproj

# Copy the rest of the code
COPY . .

# Build the app to a folder named /app/publish
RUN dotnet publish src/Api/Api.csproj -c Release -o /app/publish

# Stage 2: Run the App
# We use a smaller "Runtime" image to keep the container light
FROM mcr.microsoft.com/dotnet/aspnet:10.0
WORKDIR /app
COPY --from=build /app/publish .
EXPOSE 8080
ENTRYPOINT ["dotnet", "Api.dll"]
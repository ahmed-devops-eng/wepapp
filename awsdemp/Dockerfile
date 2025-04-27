# Step 1: Build the application
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy project file and restore dependencies
COPY awsdemp.csproj ./
RUN dotnet restore

# Copy everything and build the release
COPY . .
RUN dotnet publish -c Release -o out

# Step 2: Create the runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app

# Copy built app from build stage
COPY --from=build /app/out .

# Expose port
EXPOSE 5000

# Start the application
ENTRYPOINT ["dotnet", "awsdemp.dll"]


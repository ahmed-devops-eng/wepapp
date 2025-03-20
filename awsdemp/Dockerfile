#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["awsdemp/awsdemp.csproj", "awsdemp/"]
RUN dotnet restore "awsdemp/awsdemp.csproj"
COPY . .
WORKDIR "/src/awsdemp"
RUN dotnet build "awsdemp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "awsdemp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "awsdemp.dll"]
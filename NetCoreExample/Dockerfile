# First we add a dotnet SDK image to build our app inside the container
FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
WORKDIR /app
COPY --from=build-env /app/out .
ENV ASPNETCORE_URLS http://*:8088
EXPOSE 8088

ENTRYPOINT ["dotnet", "NetCoreExample.dll"]
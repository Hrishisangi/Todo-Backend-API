# Use the official .NET 8 SDK image
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY *.sln .
COPY ToDoApi/*.csproj ./ToDoApi/
RUN dotnet restore ToDoApi/ToDoApi.csproj

# Copy everything else and build
COPY . .
RUN dotnet publish ToDoApi/ToDoApi.csproj -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app/out .

ENTRYPOINT ["dotnet", "ToDoApi.dll"]

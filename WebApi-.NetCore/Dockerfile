#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

# FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
# USER app
# WORKDIR /app
# EXPOSE 8080
# EXPOSE 8081

# FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
# ARG BUILD_CONFIGURATION=Release
# WORKDIR /src
# RUN ls
# COPY ["WebApi-.NetCore.csproj", "WebApi-.NetCore/"]
# RUN dotnet restore "WebApi-.NetCore/WebApi-.NetCore.csproj"
# COPY . .
# # WORKDIR "/src/WebApi-.NetCore"
# RUN dotnet build "./WebApi-.NetCore.csproj" -c $BUILD_CONFIGURATION -o /app/build

# FROM build AS publish
# ARG BUILD_CONFIGURATION=Release
# RUN dotnet publish "./WebApi-.NetCore.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

# FROM base AS final
# WORKDIR /app
# COPY --from=publish /app/publish .
# ENTRYPOINT ["dotnet", "WebApi-.NetCore.dll"]

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app
COPY *.csproj ./
RUN dotnet restore
COPY . ./
RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
EXPOSE 8080
COPY --from=build /app/out .
ENTRYPOINT [ "dotnet", "WebApi-.NetCore.dll" ]
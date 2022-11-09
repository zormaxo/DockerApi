# Get base SDK image from microsoft
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build-env
WORKDIR /app

# Copy the CSPROJ file and restore any dependencies (via NUGET)
COPY *.csproj ./ 
RUN dotnet restore

# Copy the project files and build our release
COPY . .
RUN dotnet publish -c Release -o out

# Generate runtime image
FROM mcr.microsoft.com/dotnet/aspnet:7.0
WORKDIR /app
#EXPOSE 80
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "DockerApi.dll"]

#FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
#WORKDIR /app
#EXPOSE 80
#EXPOSE 443
#
#FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
#WORKDIR /src
#COPY ["DockerApi/DockerApi.csproj", "DockerApi/"]
#RUN dotnet restore "DockerApi/DockerApi.csproj"
#COPY . .
#WORKDIR "/src/DockerApi"
#RUN dotnet build "DockerApi.csproj" -c Release -o /app/build
#
#FROM build AS publish
#RUN dotnet publish "DockerApi.csproj" -c Release -o /app/publish /p:UseAppHost=false
#
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "DockerApi.dll"]
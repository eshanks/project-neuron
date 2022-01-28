#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/Geocoding/Geocoding.Service/Geocoding.Service.csproj", "src/Geocoding/Geocoding.Service/"]
RUN dotnet restore "src/Geocoding/Geocoding.Service/Geocoding.Service.csproj"
COPY . .
WORKDIR "/src/src/Geocoding/Geocoding.Service"
RUN dotnet build "Geocoding.Service.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Geocoding.Service.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Geocoding.Service.dll"]
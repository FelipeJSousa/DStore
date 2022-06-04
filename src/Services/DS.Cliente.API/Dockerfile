#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["src/Services/DS.Cliente.API/DS.Cliente.API.csproj", "src/Services/DS.Cliente.API/"]
RUN dotnet restore "src/Services/DS.Cliente.API/DS.Cliente.API.csproj"
COPY . .
WORKDIR "/src/src/Services/DS.Cliente.API"
RUN dotnet build "DS.Cliente.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DS.Cliente.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DS.Cliente.API.dll"]
#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["src/Services/DS.Pagamento.API/DS.Pagamento.API.csproj", "src/Services/DS.Pagamento.API/"]
RUN dotnet restore "src/Services/DS.Pagamento.API/DS.Pagamento.API.csproj"
COPY . .
WORKDIR "/src/src/Services/DS.Pagamento.API"
RUN dotnet build "DS.Pagamento.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DS.Pagamento.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DS.Pagamento.API.dll"]
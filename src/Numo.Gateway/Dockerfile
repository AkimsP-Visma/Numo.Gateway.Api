FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Numo.Gateway/Numo.Gateway.csproj", "Numo.Gateway/"]
RUN dotnet restore "Numo.Gateway/Numo.Gateway.csproj"
COPY . .
WORKDIR "/src/Numo.Gateway"
RUN dotnet build "Numo.Gateway.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Numo.Gateway.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Numo.Gateway.dll"]

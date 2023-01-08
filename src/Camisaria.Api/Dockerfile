FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/Camisaria.Api/Camisaria.Api.csproj", "src/Camisaria.Api/"]
RUN dotnet restore "src/Camisaria.Api/Camisaria.Api.csproj"
COPY . .
WORKDIR "/src/src/Camisaria.Api"
RUN dotnet build "Camisaria.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Camisaria.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Camisaria.Api.dll"]

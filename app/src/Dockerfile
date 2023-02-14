FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["PedeLogo.Catalogo.Api/PedeLogo.Catalogo.Api.csproj", "PedeLogo.Catalogo.Api/"]
RUN dotnet restore "PedeLogo.Catalogo.Api/PedeLogo.Catalogo.Api.csproj"
COPY . .
WORKDIR "/src/PedeLogo.Catalogo.Api"
RUN dotnet build "PedeLogo.Catalogo.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PedeLogo.Catalogo.Api.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PedeLogo.Catalogo.Api.dll"]
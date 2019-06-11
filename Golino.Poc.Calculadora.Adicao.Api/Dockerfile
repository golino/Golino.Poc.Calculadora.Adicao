FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["Golino.Poc.Calculadora.Adicao.Api/Golino.Poc.Calculadora.Adicao.Api.csproj", "Golino.Poc.Calculadora.Adicao.Api/"]
RUN dotnet restore "Golino.Poc.Calculadora.Adicao.Api/Golino.Poc.Calculadora.Adicao.Api.csproj"
COPY . .
WORKDIR "/src/Golino.Poc.Calculadora.Adicao.Api"
RUN dotnet build "Golino.Poc.Calculadora.Adicao.Api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Golino.Poc.Calculadora.Adicao.Api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Golino.Poc.Calculadora.Adicao.Api.dll"]
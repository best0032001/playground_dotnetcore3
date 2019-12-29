FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY [".", "."]
RUN dotnet restore "api_playground.csproj"
COPY . .
WORKDIR "/src"
RUN dotnet build "api_playground.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "api_playground.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "api_playground.dll"]
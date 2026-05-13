# ===== Etapa 1: Build =====
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /app

COPY *.sln ./
COPY . ./

RUN dotnet restore
RUN dotnet publish Backend.API/Backend.API.csproj -c Release -o /out

# ===== Etapa 2: Runtime =====
FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS runtime
WORKDIR /app

COPY --from=build /out ./

ENV ASPNETCORE_ENVIRONMENT=Production
ENV ASPNETCORE_URLS=http://+:$PORT

EXPOSE 8080

ENTRYPOINT ["dotnet", "Backend.API.dll"]
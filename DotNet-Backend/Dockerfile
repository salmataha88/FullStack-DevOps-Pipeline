# ===== Stage 1: Build =====
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS builder

WORKDIR /src

# Copy csproj first (cache dependencies restore)
COPY API.csproj ./

RUN dotnet restore

COPY . ./

RUN dotnet publish -c Release -o /app/publish

# ===== Stage 2: Runtime =====
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime

WORKDIR /app

# Set the ASP.NET Core URL to listen on port 8080 for nginx reverse proxy
ENV ASPNETCORE_URLS=http://+:8080

COPY --from=builder /app/publish .

EXPOSE 8080

ENTRYPOINT ["dotnet", "API.dll"]
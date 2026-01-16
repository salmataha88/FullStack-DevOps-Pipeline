FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime

WORKDIR /app

# Copy published files from CI pipeline
COPY ./build_output .

EXPOSE 8080

ENTRYPOINT ["dotnet", "Api.dll"]
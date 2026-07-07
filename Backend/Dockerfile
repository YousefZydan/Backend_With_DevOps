# المرحلة الأولى: Build
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src

COPY Clinic/Clinic.csproj Clinic/
COPY Application/Application.csproj Application/
COPY Infrastructure/Infrastructure.csproj Infrastructure/
COPY Domain/Domain.csproj Domain/

RUN dotnet restore Clinic/Clinic.csproj

COPY . .

WORKDIR /src/Clinic
RUN dotnet publish -c Release -o /app/publish

# المرحلة التانية: Runtime
FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish .

EXPOSE 8080
ENTRYPOINT ["dotnet", "Clinic.dll"]

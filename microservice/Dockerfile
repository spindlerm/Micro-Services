FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["microservice/microservice.csproj", "microservice/"]
RUN dotnet restore "microservice/microservice.csproj"
COPY . .
WORKDIR "/src/microservice"
RUN dotnet build "microservice.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "microservice.csproj" -c Release -o /app/publish

FROM base AS final
EXPOSE 80
EXPOSE 443
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "microservice.dll"]

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["orchestrationapi.csproj", "./"]
RUN dotnet restore "./orchestrationapi.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "orchestrationapi.csproj" -c Release -o /app/build
FROM build AS publish
RUN dotnet publish "orchestrationapi.csproj" -c Release -o /app/publish /p:UseAppHost=false
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "orchestrationapi.dll"]


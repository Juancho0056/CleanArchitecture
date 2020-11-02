FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 61846

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["/WebUI/WebUI.csproj", "./"]
RUN dotnet restore "./WebUI/WebUI.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "/WebUI/WebUI.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "/WebUI/WebUI.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CleanArchitecture.WebUI.dll"]
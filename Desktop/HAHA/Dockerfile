FROM mcr.microsoft.com/dotnet/core/aspnet:3.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.0 AS build
WORKDIR /src
COPY ["HelloAspNetCore.csproj", "./"]
RUN dotnet restore "./HelloAspNetCore.csproj"
COPY . .
RUN dotnet build "HelloAspNetCore.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "HelloAspNetCore.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "HelloAspNetCore.dll"]

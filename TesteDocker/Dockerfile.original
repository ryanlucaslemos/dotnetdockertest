#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /src
COPY ["TesteDocker/TesteDocker.csproj", "TesteDocker/"]
RUN dotnet restore "TesteDocker/TesteDocker.csproj"
COPY . .
WORKDIR "/src/TesteDocker"
RUN dotnet build "TesteDocker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TesteDocker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TesteDocker.dll"]
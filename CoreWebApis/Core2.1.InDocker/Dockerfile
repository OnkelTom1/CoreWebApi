#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Core2.1.InDocker/Core2.1.InDocker.csproj", "Core2.1.InDocker/"]
RUN dotnet restore "Core2.1.InDocker/Core2.1.InDocker.csproj"
COPY . .
WORKDIR "/src/Core2.1.InDocker"
RUN dotnet build "Core2.1.InDocker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Core2.1.InDocker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Core2.1.InDocker.dll"]
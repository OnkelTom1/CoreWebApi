#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["Core_2_1_InDocker/Core_2_1_InDocker.csproj", "Core_2_1_InDocker/"]
RUN dotnet restore "Core_2_1_InDocker/Core_2_1_InDocker.csproj"
COPY . .
WORKDIR "/src/Core_2_1_InDocker"
RUN dotnet build "Core_2_1_InDocker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Core_2_1_InDocker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Core_2_1_InDocker.dll"]
#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["RSoft.Monitoring.Web.PanelCheck/RSoft.Monitoring.Web.PanelCheck.csproj", "RSoft.Monitoring.Web.PanelCheck/"]
RUN dotnet restore "RSoft.Monitoring.Web.PanelCheck/RSoft.Monitoring.Web.PanelCheck.csproj"
COPY . .
WORKDIR "/src/RSoft.Monitoring.Web.PanelCheck"
RUN dotnet build "RSoft.Monitoring.Web.PanelCheck.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "RSoft.Monitoring.Web.PanelCheck.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "RSoft.Monitoring.Web.PanelCheck.dll"]
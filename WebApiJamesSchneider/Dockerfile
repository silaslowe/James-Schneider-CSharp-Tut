FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["WebApi-JamesSchneider/WebApi-JamesSchneider.csproj", "WebApi-JamesSchneider/"]
RUN dotnet restore "WebApi-JamesSchneider/WebApi-JamesSchneider.csproj"
COPY . .
WORKDIR "/src/WebApi-JamesSchneider"
RUN dotnet build "WebApi-JamesSchneider.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApi-JamesSchneider.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApi-JamesSchneider.dll"]

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["InfoSoft/Server", "Server/"]
COPY ["InfoSoft/Client", "Client/"]
COPY ["InfoSoft/Shared", "Shared/"]
RUN dotnet restore "Server/InfoSoft.Server.csproj"
COPY . .
WORKDIR "/src/Server"
RUN dotnet build "InfoSoft.Server.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "InfoSoft.Server.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "InfoSoft.Server.dll"]
    
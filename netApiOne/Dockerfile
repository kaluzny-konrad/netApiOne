FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["netApiOne/netApiOne.csproj", "netApiOne/"]
RUN dotnet restore "netApiOne/netApiOne.csproj"
COPY . .
WORKDIR "/src/netApiOne"
RUN dotnet build "netApiOne.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "netApiOne.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "netApiOne.dll"]
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["LinYangTest-01/LinYangTest-01.csproj", "LinYangTest-01/"]
RUN dotnet restore "LinYangTest-01/LinYangTest-01.csproj"
COPY . .
WORKDIR "/src/LinYangTest-01"
RUN dotnet build "LinYangTest-01.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "LinYangTest-01.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "LinYangTest-01.dll"]
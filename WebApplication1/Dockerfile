FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 5021

ENV ASPNETCORE_URLS=http://+:5021

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["WebApplication1/TestWebApplication.csproj", "WebApplication1/"]
RUN dotnet restore "WebApplication1\TestWebApplication.csproj"
COPY . .
WORKDIR "/src/WebApplication1"
RUN dotnet build "TestWebApplication.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TestWebApplication.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TestWebApplication.dll"]

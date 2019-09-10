FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["MVCDemo/MVCDemo.csproj", "MVCDemo/"]
RUN dotnet restore "MVCDemo/MVCDemo.csproj"
COPY . .
WORKDIR "/src/MVCDemo"
RUN dotnet build "MVCDemo.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MVCDemo.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MVCDemo.dll"]
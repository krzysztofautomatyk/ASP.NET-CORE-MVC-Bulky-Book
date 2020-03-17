#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["ASP.NET-CORE-MVC-Bulky-Book/ASP.NET-CORE-MVC-Bulky-Book.csproj", "ASP.NET-CORE-MVC-Bulky-Book/"]
RUN dotnet restore "ASP.NET-CORE-MVC-Bulky-Book/ASP.NET-CORE-MVC-Bulky-Book.csproj"
COPY . .
WORKDIR "/src/ASP.NET-CORE-MVC-Bulky-Book"
RUN dotnet build "ASP.NET-CORE-MVC-Bulky-Book.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ASP.NET-CORE-MVC-Bulky-Book.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ASP.NET-CORE-MVC-Bulky-Book.dll"]
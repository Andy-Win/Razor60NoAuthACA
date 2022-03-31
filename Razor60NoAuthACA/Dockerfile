#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Razor60NoAuthACA/Razor60NoAuthACA.csproj", "Razor60NoAuthACA/"]
RUN dotnet restore "Razor60NoAuthACA/Razor60NoAuthACA.csproj"
COPY . .
WORKDIR "/src/Razor60NoAuthACA"
RUN dotnet build "Razor60NoAuthACA.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Razor60NoAuthACA.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Razor60NoAuthACA.dll"]
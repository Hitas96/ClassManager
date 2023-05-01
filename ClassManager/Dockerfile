#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["ClassManager/ClassManager.csproj", "ClassManager/"]
RUN dotnet restore "ClassManager/ClassManager.csproj"
COPY . .
WORKDIR "/src/ClassManager"
RUN dotnet build "ClassManager.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ClassManager.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ClassManager.dll"]
#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["StudentsManagement.API/StudentsManagement.API.csproj", "StudentsManagement.API/"]
RUN dotnet restore "StudentsManagement.API/StudentsManagement.API.csproj"
COPY . .
WORKDIR "/src/StudentsManagement.API"
RUN dotnet build "StudentsManagement.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "StudentsManagement.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "StudentsManagement.API.dll"]
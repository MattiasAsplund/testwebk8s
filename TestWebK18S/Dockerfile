#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["TestWebK18S/TestWebK18S.csproj", "TestWebK18S/"]
RUN dotnet restore "TestWebK18S/TestWebK18S.csproj"
COPY . .
WORKDIR "/src/TestWebK18S"
RUN dotnet build "TestWebK18S.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TestWebK18S.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TestWebK18S.dll"]
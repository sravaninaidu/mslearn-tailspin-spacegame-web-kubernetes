FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
ENV ASPNETCORE_URLS=http://+:8080
EXPOSE 8080

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["Tailspin.SpaceGame.Web/Tailspin.SpaceGame.Web.csproj", "Tailspin.SpaceGame.Web/"]

RUN dotnet restore "Tailspin.SpaceGame.Web/Tailspin.SpaceGame.Web.csproj"
COPY . .
WORKDIR "/src/Tailspin.SpaceGame.Web"
RUN dotnet build "Tailspin.SpaceGame.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Tailspin.SpaceGame.Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Tailspin.SpaceGame.Web.dll"]

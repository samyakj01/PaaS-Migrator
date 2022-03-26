FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["./BookListMVC.csproj", "BookListMVC/"]
RUN dotnet restore "BookListMVC/BookListMVC.csproj"

WORKDIR "/src/BookListMVC"
COPY . .
RUN dotnet build "BookListMVC.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BookListMVC.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BookListMVC.dll"]
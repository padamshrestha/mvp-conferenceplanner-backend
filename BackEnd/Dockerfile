FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY BackEnd.csproj .
RUN dotnet restore -nowarn:msb3202,nu1503
COPY . .
RUN dotnet build BackEnd.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish BackEnd.csproj -c Release -o /app

FROM base AS final
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "BackEnd.dll"]

FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 60096
EXPOSE 44301

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY StrengthSheets/StrengthSheets.csproj StrengthSheets/
RUN dotnet restore StrengthSheets/StrengthSheets.csproj
COPY . .
WORKDIR /src/StrengthSheets
RUN dotnet build StrengthSheets.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish StrengthSheets.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "StrengthSheets.dll"]

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
COPY ./WebApp.csproj ./
RUN dotnet restore ./WebApp.csproj
COPY . .
RUN dotnet publish ./WebApp.csproj -c Release -o /app --no-restore

FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS final
WORKDIR /app
ENV ASPNETCORE_URLS=http://+:8080 DOTNET_RUNNING_IN_CONTAINER=true
COPY --from=build /app ./
EXPOSE 8080
ENTRYPOINT ["dotnet","WebApp.dll"]
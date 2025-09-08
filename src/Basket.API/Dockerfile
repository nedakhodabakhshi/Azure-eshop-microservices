FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
COPY ./Basket.API.csproj ./
RUN dotnet restore ./Basket.API.csproj
COPY . .
RUN dotnet publish ./Basket.API.csproj -c Release -o /app --no-restore

FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS final
WORKDIR /app
ENV ASPNETCORE_URLS=http://+:8080 DOTNET_RUNNING_IN_CONTAINER=true
COPY --from=build /app ./
EXPOSE 8080
ENTRYPOINT ["dotnet","Basket.API.dll"]
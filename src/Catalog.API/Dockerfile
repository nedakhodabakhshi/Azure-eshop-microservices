# ---------- Build ----------
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src

# Copy only csproj first (better cache)
COPY ./Catalog.API.csproj ./
RUN dotnet restore ./Catalog.API.csproj

# Now copy the rest
COPY . .

# Publish (no restore again)
RUN dotnet publish ./Catalog.API.csproj -c Release -o /app --no-restore

# ---------- Runtime ----------
FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS final
WORKDIR /app

# Make ASP.NET listen on 8080 inside container
ENV ASPNETCORE_URLS=http://+:8080 \
    DOTNET_RUNNING_IN_CONTAINER=true

COPY --from=build /app ./
EXPOSE 8080
ENTRYPOINT ["dotnet","Catalog.API.dll"]

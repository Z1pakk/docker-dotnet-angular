#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src

COPY ["MoviesAPI/MoviesAPI.csproj", "MoviesAPI/"]
COPY ["Movies.Shared/Movies.Shared.csproj", "Movies.Shared/"]

RUN dotnet restore "MoviesAPI/MoviesAPI.csproj"
COPY . .

WORKDIR "/src/MoviesAPI"
RUN dotnet build "MoviesAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MoviesAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MoviesAPI.dll"]

# from angular-dotnet-sample
# docker build -t movies-api:dev -f ./MoviesAPI/Dockerfile .
# docker run -d -p 5001:80 movies-api:dev --name movies-api

# to see docker files: docker exec -it <container-id> /bin/sh
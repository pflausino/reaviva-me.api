FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY *.sln .
COPY src/ReavivaMe.Api/*.csproj ./ReavivaMe.Api/
COPY src/ReavivaMe.Domain/*.csproj ./ReavivaMe.Domain/
COPY src/ReavivaMe.Infra/*.csproj ./ReavivaMe.Infra/
COPY src/ReavivaMe.Api.Tests/*.csproj ./ReavivaMe.Api.Tests/
COPY src/ReavivaMe.Domain.Tests/*.csproj ./ReavivaMe.Domain.Tests/ 
#
RUN dotnet restore 
#
# copy everything else and build app
COPY src/ReavivaMe.Api/. ./ReavivaMe.Api/
COPY src/ReavivaMe.Domain/. ./ReavivaMe.Domain/
COPY src/ReavivaMe.Infra/. ./ReavivaMe.Infra/ 
#
WORKDIR /app/ReavivaMe.Api
RUN dotnet publish -c Release -o out 
#
FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS runtime
WORKDIR /app 

COPY --from=build /app/ReavivaMe.Api/out ./
ENTRYPOINT ["dotnet", "ReavivaMe.Api.dll"]

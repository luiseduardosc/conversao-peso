#https://hub.docker.com/_/microsoft-dotnet-sdk/
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /app

#copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

#copy everything else and build app
COPY . ./
RUN dotnet publish -c release -o /app -no-restore

#https://hub.docker.com/_/microsoft-dotnet-aspnet
#final stage/image
FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS final
WORKDIR /app
COPY --from=build /app ./
ENTRYPOINT ["dotnet", "ConversaoPeso.Web.dll"]

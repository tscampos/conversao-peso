FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["ConversaoPeso.Web.csproj", "src/ConversaoPeso.Web/"]
RUN dotnet restore "src/ConversaoPeso.Web/ConversaoPeso.Web.csproj"
COPY . .
WORKDIR "/src/src/ConversaoPeso.Web"
RUN dotnet build "ConversaoPeso.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ConversaoPeso.Web.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS final
WORKDIR /app
EXPOSE 80
EXPOSE 443
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ConversaoPeso.Web.dll"]





# FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
# WORKDIR /app

# COPY *.csproj ./
# RUN dotnet restore

# COPY ./ ./
# RUN dotnet publish -c release -o out

# FROM mcr.microsoft.com/dotnet/aspnet:5.0
# WORKDIR /app
# COPY --from=build /app/out ./
# ENTRYPOINT ["dotnet", "ConversaoPeso.Web.dll"]

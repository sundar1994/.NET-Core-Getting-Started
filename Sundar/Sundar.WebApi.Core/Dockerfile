FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["Sundar.WebApi.Core/Sundar.WebApi.Core.csproj", "Sundar.WebApi.Core/"]
RUN dotnet restore "Sundar.WebApi.Core/Sundar.WebApi.Core.csproj"
COPY . .
WORKDIR "/src/Sundar.WebApi.Core"
RUN dotnet build "Sundar.WebApi.Core.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Sundar.WebApi.Core.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Sundar.WebApi.Core.dll"]
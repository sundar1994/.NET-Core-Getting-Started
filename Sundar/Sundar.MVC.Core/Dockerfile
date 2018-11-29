FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["Sundar.MVC.Core/Sundar.MVC.Core.csproj", "Sundar.MVC.Core/"]
RUN dotnet restore "Sundar.MVC.Core/Sundar.MVC.Core.csproj"
COPY . .
WORKDIR "/src/Sundar.MVC.Core"
RUN dotnet build "Sundar.MVC.Core.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Sundar.MVC.Core.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Sundar.MVC.Core.dll"]
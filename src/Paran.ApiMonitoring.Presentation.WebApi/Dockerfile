FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 15163
EXPOSE 44330

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["src/Paran.ApiMonitoring.Presentation.WebApi/Paran.ApiMonitoring.Presentation.WebApi.csproj", "src/Paran.ApiMonitoring.Presentation.WebApi/"]
RUN dotnet restore "src/Paran.ApiMonitoring.Presentation.WebApi/Paran.ApiMonitoring.Presentation.WebApi.csproj"
COPY . .
WORKDIR "/src/src/Paran.ApiMonitoring.Presentation.WebApi"
RUN dotnet build "Paran.ApiMonitoring.Presentation.WebApi.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Paran.ApiMonitoring.Presentation.WebApi.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Paran.ApiMonitoring.Presentation.WebApi.dll"]
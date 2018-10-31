FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["Kubernetes_Microservices/Kubernetes_Microservices.csproj", "Kubernetes_Microservices/"]

RUN dotnet restore "$PROJECT_DIR/Kubernetes_Microservices.csproj"
COPY . .
WORKDIR "/src/Kubernetes_Microservices"
RUN dotnet build "Kubernetes_Microservices.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Kubernetes_Microservices.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Kubernetes_Microservices.dll"]
FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 55639
EXPOSE 44316

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["../CakeShop.PresentationLayer/CakeShop.PresentationLayer.csproj", "../CakeShop.PresentationLayer/"]
RUN dotnet restore "../CakeShop.PresentationLayer/CakeShop.PresentationLayer.csproj"
COPY . .
WORKDIR "/src/../CakeShop.PresentationLayer"
RUN dotnet build "CakeShop.PresentationLayer.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "CakeShop.PresentationLayer.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CakeShop.PresentationLayer.dll"]
FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["InventarioPatrimonial/InventarioPatrimonial.csproj", "InventarioPatrimonial/"]
COPY ["Servicos/Servicos.csproj", "Servicos/"]
COPY ["Infraestrutura/Infraestrutura.csproj", "Infraestrutura/"]
COPY ["Negocio/Negocio.csproj", "Negocio/"]
RUN dotnet restore "InventarioPatrimonial/InventarioPatrimonial.csproj"
COPY . .
WORKDIR "/src/InventarioPatrimonial"
RUN dotnet build "InventarioPatrimonial.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "InventarioPatrimonial.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "InventarioPatrimonial.dll"]
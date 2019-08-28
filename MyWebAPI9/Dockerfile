FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 60233
EXPOSE 44330

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["MyWebAPI9/MyWebAPI9.csproj", "MyWebAPI9/"]
RUN dotnet restore "MyWebAPI9/MyWebAPI9.csproj"
COPY . .
WORKDIR "/src/MyWebAPI9"
RUN dotnet build "MyWebAPI9.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MyWebAPI9.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MyWebAPI9.dll"]
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["LearnASP/LearnASP.csproj", "LearnASP/"]
RUN dotnet restore "LearnASP/LearnASP.csproj"
COPY . .
WORKDIR "/src/LearnASP"
RUN dotnet build "LearnASP.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "LearnASP.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "LearnASP.dll"]

FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["SoftplanCalcTest/SoftplanCalcTest.csproj", "SoftplanCalcTest/"]
RUN dotnet restore "SoftplanCalcTest/SoftplanCalcTest.csproj"
COPY . .
WORKDIR "/src/SoftplanCalcTest"
RUN dotnet build "SoftplanCalcTest.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "SoftplanCalcTest.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SoftplanCalcTest.dll"]
FROM mcr.microsoft.com/dotnet/aspnet AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk AS build
WORKDIR /src
COPY ["CrispyEnigma.API/CrispyEnigma.API.csproj", "CrispyEnigma.API/"]
RUN dotnet restore "CrispyEnigma.API/CrispyEnigma.API.csproj"
COPY . .
WORKDIR "/src/CrispyEnigma.API"
RUN dotnet build "CrispyEnigma.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CrispyEnigma.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CrispyEnigma.API.dll"]

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["TemplateProjects/TemplateProjects.csproj", "TemplateProjects/"]
RUN dotnet restore "TemplateProjects/TemplateProjects.csproj"
COPY . .
WORKDIR "/src/TemplateProjects"
RUN dotnet build "TemplateProjects.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TemplateProjects.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TemplateProjects.dll"]

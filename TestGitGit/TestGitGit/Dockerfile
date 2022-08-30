FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["TestGitGit/TestGitGit.csproj", "TestGitGit/"]
RUN dotnet restore "TestGitGit/TestGitGit.csproj"
COPY . .
WORKDIR "/src/TestGitGit"
RUN dotnet build "TestGitGit.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TestGitGit.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TestGitGit.dll"]

FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/MessageProcessorConsoleService/MessageProcessorConsoleService.csproj", "MessageProcessorConsoleService/"]
COPY ["src/Core/Core.csproj", "Core/"]
RUN dotnet restore "MessageProcessorConsoleService/MessageProcessorConsoleService.csproj"
COPY . .
WORKDIR "/src/src/MessageProcessorConsoleService"
RUN dotnet build "MessageProcessorConsoleService.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MessageProcessorConsoleService.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MessageProcessorConsoleService.dll"]
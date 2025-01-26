#docker build --platform linux/arm64 -t babajuneed/examplevotingapp_worker . 
FROM --platform=$BUILDPLATFORM mcr.microsoft.com/dotnet/core/sdk:3.1 as builder

WORKDIR /Worker
COPY src/Worker/Worker.csproj .
RUN dotnet restore

COPY src/Worker/ .
RUN dotnet publish -c Release -o /out Worker.csproj

# app image
FROM --platform=$BUILDPLATFORM mcr.microsoft.com/dotnet/core/runtime:3.1

WORKDIR /app
ENTRYPOINT ["dotnet", "Worker.dll"]

COPY --from=builder /out .
FROM microsoft/aspnetcore-build AS build-env

WORKDIR /app
COPY *.csproj ./
RUN dotnet restore

COPY . .

RUN dotnet publish -c Release -o out

# Build runtime image
FROM microsoft/aspnetcore:2.0
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "source.dll"]
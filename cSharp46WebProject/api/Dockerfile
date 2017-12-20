FROM nugardt/msbuild:15.0 as builder
SHELL ["powershell"]

WORKDIR /build

COPY . ./

RUN ["nuget.exe", "restore"]
RUN ["msbuild.exe", "api.sln", "/p:Configuration=Release", "/m", "/p:DeployOnBuild=true", "/p:PublishProfile=FolderProfile"]

FROM microsoft/aspnet
SHELL ["powershell"]
WORKDIR /app

RUN Remove-WebSite -Name 'Default Web Site';

RUN mkdir /site

RUN Import-module IISAdministration;\
    New-IISSite -Name "Site" -PhysicalPath C:\site -BindingInformation "*:8000:"

EXPOSE 8000

COPY --from=builder /build/api/bin/Release/PublishOutput /site

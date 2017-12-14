FROM nugardt/msbuild:15.0 as builder
SHELL ["powershell"]

WORKDIR /build

COPY . ./

RUN ["nuget.exe", "restore"]
RUN ["msbuild.exe", "api.sln", "/p:Configuration=Release", "/m"]

FROM microsoft/iis
SHELL ["powershell"]
WORKDIR /app

RUN Install-WindowsFeature NET-Framework-45-ASPNET; Install-WindowsFeature Web-Asp-Net45; Import-module IISAdministration; Remove-WebSite -Name 'Default Web Site';

RUN New-IISSite -Name 'application' -PhysicalPath 'c:/app' -BindingInformation '*:80:' -Force

EXPOSE 80

COPY --from=builder /build/api/bin .
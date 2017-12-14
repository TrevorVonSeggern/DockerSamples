FROM nugardt/msbuild:15.0
SHELL ["powershell"]

WORKDIR /build

COPY . ./

RUN ["nuget.exe", "restore"]
RUN ["msbuild.exe", "dotnetApp-4.sln", "/p:Configuration=Release", "/m"]

# RUN ["msbuild.exe", "./dotnetApp-4.csproj", "/p:Configuration=Release"]
RUN ls bin/Release
ENTRYPOINT [ "bin/Release/dotnetapp-4.62.exe" ]
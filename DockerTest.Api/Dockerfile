FROM microsoft/dotnet:2.0-sdk AS build
WORKDIR /app

# copy csproj and restore as distinct layers
#COPY *.sln .
COPY ./*.csproj ./
#COPY utils/*.csproj ./utils/
#COPY tests/*.csproj ./tests/
RUN dotnet restore

# copy and build everything else
COPY . ./
#COPY utils/. ./utils/
#COPY tests/. ./tests/

RUN dotnet build

#FROM build AS testrunner
#WORKDIR /app/tests
#ENTRYPOINT ["dotnet", "test","--logger:trx"]

#FROM build AS test
#WORKDIR /app/tests
#RUN dotnet test

FROM build AS publish
RUN dotnet publish -o out

FROM microsoft/dotnet:2.0-runtime AS runtime
WORKDIR /app
COPY --from=publish /app/out ./
ENTRYPOINT ["dotnet", "DockerTest.Api.dll"]
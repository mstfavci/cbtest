#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["cbunittest/cbunittest.csproj", "cbunittest/"]
COPY ["cbtest/cbtest.csproj", "cbtest/"]
RUN dotnet restore "cbunittest/cbunittest.csproj"
COPY . .


WORKDIR "/src/cbunittest"
RUN dotnet build "cbunittest.csproj" -c Release -o /app/build


# run tests on docker build
RUN dotnet test

# run tests on docker run
ENTRYPOINT ["dotnet", "test"]


#FROM build AS publish2
#RUN dotnet test

#FROM build AS publish
#RUN dotnet publish "cbunittest.csproj" -c Release -o /app/publish

#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "cbunittest.dll"]


ARG IMAGE_BASE=6.0-alpine


FROM mcr.microsoft.com/dotnet/sdk:$IMAGE_BASE as build
WORKDIR /build

# Copy project source files     , currently only work for linux (docker2node is your jenkins pipeline name). Window or Linux still can use ' COPY src ./src '
COPY src ./src      


WORKDIR /build/src
RUN dotnet restore
RUN dotnet publish --no-restore --configuration Release


#stage 2
# Base image is .NET Core runtime only (Linux)
FROM mcr.microsoft.com/dotnet/aspnet:$IMAGE_BASE


LABEL org.label-schema.name=".NET Core Demo Web App" \
      org.label-schema.version="1.5.0" \
      org.label-schema.vendor="Ben Coleman" \
      org.opencontainers.image.source="https://github.com/benc-uk/dotnet-demoapp"

WORKDIR /app

COPY --from=build /build/src/bin/Release/net6.0/publish/ .

EXPOSE 5000

ENV ASPNETCORE_URLS http://*:5000
ENV ASPNETCORE_ENVIRONMENT Production
# This is critical for the Azure AD signin flow to work in Kubernetes and App Service
ENV ASPNETCORE_FORWARDEDHEADERS_ENABLED=true

# Run the ASP.NET Core app
ENTRYPOINT dotnet dotnet-demoapp.dll
FROM mcr.microsoft.com/windows/servercore/iis:windowsservercore-ltsc2019

RUN powershell.exe -Command \
  Set-ExecutionPolicy Bypass -Scope Process ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-WebServerRole ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-WebServer ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-CommonHttpFeatures ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-HttpErrors ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-HttpRedirect ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-ApplicationDevelopment ; \
  Enable-WindowsOptionalFeature -online -FeatureName NetFx4Extended-ASPNET45 ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-NetFxExtensibility45 ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-HealthAndDiagnostics ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-HttpLogging ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-LoggingLibraries ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-RequestMonitor ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-HttpTracing ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-Security ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-RequestFiltering ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-Performance ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-Security ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-BasicAuthentication ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-WindowsAuthentication ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-StaticContent ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-DefaultDocument ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-WebSockets ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-ApplicationInit ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-ISAPIExtensions ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-ISAPIFilter ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-HttpCompressionStatic ; \
  Enable-WindowsOptionalFeature -Online -FeatureName IIS-ASPNET45

WORKDIR c:/inetpub/wwwroot

COPY logo.png logo.png
COPY index.html index.html
COPY script.js script.js
COPY style.css style.css

ENV GIT_VERSION 2.23
ENV GIT_PATCH_VERSION 0

RUN powershell -Command $ErrorActionPreference = 'Stop' ; \
    [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12 ; \
    Invoke-WebRequest $('https://github.com/git-for-windows/git/releases/download/v{0}.{1}.windows.1/MinGit-{0}.{1}-busybox-64-bit.zip' -f $env:GIT_VERSION, $env:GIT_PATCH_VERSION) -OutFile 'mingit.zip' -UseBasicParsing ; \
    Expand-Archive mingit.zip -DestinationPath c:\mingit ; \
    Remove-Item mingit.zip -Force ; \
    setx /M PATH $('c:\mingit\cmd;{0}' -f $env:PATH)

RUN del iisstart.*

EXPOSE 80 443
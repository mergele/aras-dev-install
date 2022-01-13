# preparing my aras dev environment

Notes on preparing my machine for local aras install, following the Article [Configuring Your Development Machine for Aras Innovator, by Eli Donahue](https://community.aras.com/b/english/posts/configuring-your-development-machine-for-aras-innovator) and asking a lot questions to my colleagues :-D.

questionmarks where I still have questions :-).

## Reference Platforms 
Machines / Environments I tested with...

### MINB01 
(Lenovo T460s)

### IN-443 
(Microsoft Surface Pro 7)
```
Gerätename           IN-443
Prozessor            Intel(R) Core(TM) i7-1065G7 CPU @ 1.30GHz   1.50 GHz
Installierter RAM    16,0 GB (15,6 GB verwendbar)
Edition:             Windows 10 enterprise
Version              21H2
Betriebssystembuild  19044.1415
Leistung             Windows Feature Experience Pack 120.2212.3920.0
```

### DEV01 
(hyperv virtual machine on IN-443)
```
Gerätename           DEV01
Prozessor            Intel(R) Core(TM) i7-1065G7 CPU @ 1.30GHz   1.50 GHz
Installierter RAM    4,00 GB (2,74 GB verwendbar)
Edition              Windows 10 Pro
Version              21H2
Betriebssystembuild  19044.1466
Leistung             Windows Feature Experience Pack 120.2212.3920.0
```

## install all the prerequisites

### winget
install the production version as app from the appstore
https://docs.microsoft.com/de-de/windows/package-manager/winget/

use
```
winget list
```
to check for installes libraries

I use `winget list > HOSTNAME-winget-list-###.txt` do document progress, usefull for debugging.

### Frameworks, Libs, ...
Ausgangszustand [dev01-winget-list](dev01-winget-list-001.txt)

Enable following features [Windows-Features aktivieren oder deaktivieren (inside Systemsteuerung)](windows-features-dotnet.png)
- [x] .NET Framework 3.5
- [x] .NET Framework 4.8 Advanced Services

[dev01-winget-list-002](dev01-winget-list-002.txt)

### .NET Framework 4.7.2
[Download .NET Framework 4.7.2](https://dotnet.microsoft.com/en-us/download/dotnet-framework/net472)
- [x] .NET Framework 4.7.2 Runtime (Installer will probably fail, because a newer version is already installed. Use [.NET Framework 4.7.2 Developer Pack installer](https://dotnet.microsoft.com/en-us/download/dotnet-framework/thank-you/net472-developer-pack-offline-installer) instead)

[dev01-winget-list-003](dev01-winget-list-003.txt)


### .NET Core 2.1.8, Runtime and Hosting Bundle
[Download .NET Core 2.1](https://dotnet.microsoft.com/en-us/download/dotnet/2.1)
- [x] ASP.NET Core Runtime 2.1.8 [Hosting Bundle](https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/runtime-aspnetcore-2.1.8-windows-hosting-bundle-installer),  contains .NET Core Runtime - 2.1.8 (x86 + x64), [dev01-winget-list-004](dev01-winget-list-004.txt)
- [x] ASP.NET Core Runtime 2.1.8 [(x64)](https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/runtime-aspnetcore-2.1.8-windows-x64-installer), [dev01-winget-list-005](dev01-winget-list-005.txt)
- [ ] ?? ASP.NET Core Runtime 2.1.8 (x86), ?? x86 needed ??
- [ ] ?? .NET Runtime 2.1.8 (x64), already inlcuded in the Hosting Bundle!
- [ ] ?? .NET Runtime 2.1.8 (x86), already inlcuded in the Hosting Bundle!

### .NET Core 3.1.8, Runtime and Hosting Bundle
[Download .NET Core 3.1](https://dotnet.microsoft.com/en-us/download/dotnet/3.1)
- [x] ASP.NET Core Runtime 3.1.8 ([Hosting Bundle](https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/runtime-aspnetcore-3.1.8-windows-hosting-bundle-installer)),  [dev01-winget-list-006](dev01-winget-list-006.txt)
- [x] ASP.NET Core Runtime 3.1.8 ([x64](https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/runtime-aspnetcore-3.1.8-windows-x64-installer)), [dev01-winget-list-007](dev01-winget-list-007.txt)
- [ ] ?? ASP.NET Core Runtime 3.1.8 (x86)
- [ ] ?? .NET Runtime 3.1.8 (x64), already inlcuded in the Hosting Bundle!
- [ ] ?? .NET Runtime 3.1.8 (x86), already inlcuded in the Hosting Bundle!

### Visual C++ Redistributable für Visual Studio 2015 
- [ ] [Visual C++ Redistributable für Visual Studio 2015](https://www.microsoft.com/de-de/download/confirmation.aspx?id=48145) (Installer will probably fail, installer will probably fail, because a newer version is already installed.
- [x] [Microsoft Visual C++ Redistributable Latest Supported Downloads](https://docs.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist) should work fine, Microsoft Visual C++ 2015 Redistributable is included. ([x64](https://aka.ms/vs/17/release/vc_redist.x64.exe)), [dev01-winget-list-008](dev01-winget-list-008.txt)

reboot.

### IIS
Enable following features [Windows-Features aktivieren oder deaktivieren (inside Systemsteuerung)](windows-features-iis.png)
- [x] Webverwaltungstools (complete, beside "Kompatibilität mit IIS 6-Verwaltung")
- [x] WWW-Dienste (complete) 
- [x] check if IIS is up and running by calling [http://localhost/](http://localhost/)

funfact: in the `winget list` output, the only change is an update of the winget packet manager itself :-D. No chance to track feature-changes this way? [dev01-winget-list-009](dev01-winget-list-009.txt)

### SQL Server Management Studio (SSMS)
[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/de-de/sql/ssms/sql-server-management-studio-ssms?view=sql-server-ver15), [Direct Download Link](https://aka.ms/ssmsfullsetup)
- [x] Install as is
 
 [dev01-winget-list-010](dev01-winget-list-010.txt)
 
### SQL Server Express
[SQL Server Express 2019](https://www.microsoft.com/de-de/sql-server/sql-server-downloads), 
- [x] [Direkt Download Link](https://go.microsoft.com/fwlink/?linkid=866658), will put SQL2019-SSEI-Expr.exe into your Download folder
- [x] Run that installer with "Medien herunterladen" first. This will place a self extractable archiv SQLEXPR_x64_DEU.exe into your Download folder
- [x] Run SQL2019-SSEI-Expr.exe will extract to SQLEXPR_x64_DEU in the same folder
- [x] From there run the SETUP.EXE to install
- [x] Choose "Neue Eigenständige Installation ... "
- [x] Let the installer search for Updates
- [x] Name your instance if you want...
- [x] Choose Mixed Mode for Authentication, so you can set the SQL Server-Systemadmin ("SA") password
- [x] Let the installer do the work

 [dev01-winget-list-011](dev01-winget-list-011.txt)

## Check
- [x] check if sql-server is up and running by connecting to database (use ssms, sa user with sql server authentication)
- [x] check if aras-innovator R12SP18 installation works out of the box


# Credits
to Eli Donahue for his work [Configuring Your Development Machine for Aras Innovator](https://community.aras.com/b/english/posts/configuring-your-development-machine-for-aras-innovator)
- to my Colleagues Clemens & Sri

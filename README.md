# espFTPServer
Simple FTP Server for the esp8266/esp32 with LittleFS and SPIFFS support.

I've modified a FTP server from arduino/wifi shield to work with the esp826. It should also work on the esp32. LittleFS with directory handling is supported since SPIFFS has been marked deprecated.
This allows you to FTP into your esp8266/esp32 and access/modify the LittleFS/SPIFFS folder/data.
I've tested it with Filezilla, and it works (upload/download/rename/delete). There's no create/modify directory support in SPIFFS but in LittleFS there is!

## Features
* Supports active and passive FTP
* Works with LittleFS and SPIFFS
* Supports Directories in LittleFS

## Limitations
* It only allows one ftp control and one data connection at a time. You need to setup Filezilla (or other clients) to respect that, i.e. only allow **1** connection. (In FileZilla go to File/Site Manager then select your site. In Transfer Settings, check "Limit number of simultaneous connections" and set the maximum to 1.)
* It does not support encryption, so you'll have to disable any form of encryption...

## Usage

### Construct an espFTPServer
Select the desired FS via the contructor 
```cpp
#include <espFTPServer.h>
#include <LittleFS.h>

FtpServer ftpSrv(LittleFS); // construct with LittleFS
// or
FtpServer ftpSrv(SPIFFS);   // construct with SPIFFS if you need to for backward compatibility
```

### Configure username/password
```cpp
ftpSrv.begin("username", "password");
```

### Handle by calling frequently
```cpp
ftpSrv.handleFTP(); // place this in e.g. loop()
```

## Notes
I forked from https://github.com/nailbuster/esp8266FTPServer which itself was forked from: https://github.com/gallegojm/Arduino-Ftp-Server/tree/master/FtpServer

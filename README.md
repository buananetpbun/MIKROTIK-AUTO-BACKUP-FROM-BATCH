# MIKROTIK-AUTO--BACKUP-FROM-BATCH
Easy backup mikrotik (.backup) only use BATCH Windows



@echo off

:: Set username and password mikrotik (with full access)
set user=admin
set pass=12345
set ip=192.168.10.1 (ip gateway)

:: Window Attributes
title EASY BACKUP MIKROTIK
mode CON: cols=55 lines=22

:: Menu
echo.
echo  ================================================
echo  EASY BACKUP MIKROTIK FROM BATCH	
echo  ================================================
echo  By: Buananet SECURE! 2019
echo  fb.com/buananet.pangkalanbun
echo  ------------------------------------------------
echo.

:: Input File Name
echo Enter File Name For Backup (without space):
set /p name="File Name = " 

:: mikrotik script
echo /system backup save name=%name%>script.backup.rsc


:: ftp commands to upload script
echo user %user%> ftp.dat
echo %pass%>> ftp.dat
echo put script.backup.rsc>> ftp.dat
echo quit>> ftp.dat

:: upload script
ftp -n -s:ftp.dat %ip%> NUL

echo.
echo  *** Backup %name%.backup on mikrotik done!
echo.

:: Question backup to PC
echo Are you sure backup to local computer?
choice /c YN
if %errorlevel%==1 goto yes
if %errorlevel%==2 goto no

:yes

echo user %user%> ftp.dat
echo %pass%>> ftp.dat
echo get %name%.backup>> ftp.dat
echo quit>> ftp.dat

:: upload script
ftp -n -s:ftp.dat %ip%> NUL

echo.
echo  *** Backup %name%.backup on PC done!
echo.

:: cleanup
del /q ftp.dat
del /q script.backup.rsc
echo.&pause&goto:eof

:no
:: cleanup
del /q ftp.dat
del /q script.backup.rsc
echo.&pause&goto:eof

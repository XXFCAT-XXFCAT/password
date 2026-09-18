@echo off
chcp 65001
title                                                                                                                                                                                                                                                                                  XXFCAT for Nova Launcher
color 5
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
goto menu

:menu
cls
echo ===================================================================================================================
echo       ┌╦═╗ ╦┐ ┌╦═══╦┐ ┌╦   ╦┐ ┌╦═══╦┐      ┌╔═╦═╗┐ ┌╦═╗ ╦┐ ┌╦═══╦┐ ┌╦═══╦┐ ┌╦═══╦┐ ┌╔═╦═╗┐ ┌╦═══╦┐ ┌╦═══╦┐
echo       │║ ║ ║│ │║   ║│ │╚╗ ╔╝│ ├╬═══╬│         ║    │║ ║ ║│      ║│ ├╬══    │║         ║    │║   ║│ │╠══╦╩┘
echo        ╩ ╚═╩┘ └╩═══╩┘ └─╚═╝─┘ └╩   ╩┘      └╚═╩═╝┘ └╩ ╚═╩┘ └╩═══╩┘ └╩═══╩┘ └╩═══╩┘    ╩    └╩═══╩┘ └╩  ╚═┘
echo ===================================================================================================================
echo.
echo 1. open Nova Menu injector  
echo.            
echo 2. open Bypass injector
echo.
echo 3. FCS Menu injector
echo.
echo 4. Open pictures folder
echo.
echo 5. Update Logs
echo.
echo 6. Open Animal Company
echo.
echo 7. Open SteamVR
echo.
echo 8. Stop Animal Company
echo.
echo 9. Stop SteamVR
echo.
echo 10. Credits
echo.
echo 11. Settings
echo.
echo 12. Exit
echo.                                         
set /p choice=Choose an option (1-12): 

if "%choice%"=="1" goto Nova Menu
if "%choice%"=="2" goto Bypass
if "%choice%"=="3" goto FCS Menu
if "%choice%"=="4" goto openAnimalFolders
if "%choice%"=="5" goto Update Logs
if "%choice%"=="6" goto OpenAnimalCompany
if "%choice%"=="7" goto openSteamVR
if "%choice%"=="8" goto StopAnimalCompany
if "%choice%"=="9" goto StopSteamVR
if "%choice%"=="10" goto credits
if "%choice%"=="11" goto settings
if "%choice%"=="12" goto exit


:Nova Menu
echo Launching Nova Menu...
timeout /t 1 >nul
cd /d "%~dp0Mods Helper" || exit /b 1
start "" cmd /k frida -l "frida-il2cpp-bridge.js" -l "symbols.ts" -l "qs-unpatchable.ts" -l "NOVA.ts" "EACLauncher.exe"
goto menu

:Bypass
echo Launching Bypass...
timeout /t 1 >nul
cd /d "%~dp0Mods Helper" || exit /b 1
start "" cmd /k py -3 "%~dp0Mods Helper\bypass.py" 
pause
goto menu

:FCS Menu
echo Launching FCS Menu...
timeout /t 1 >nul
cd /d "%~dp0Mods Helper" || exit /b 1
start "" cmd /k frida -l "frida-il2cpp-bridge.js" -l "sy.ts" -l "m4.ts" -l "da.ts" "EACLauncher.exe"
pause
goto menu

:openAnimalFolders
echo opening Animal Company folders...
timeout /t 1 >nul
start "" explorer "D:\SteamLibrary\steamapps\common\Animal Company"
goto menu

:OpenAnimalCompany
echo Launching Animal Company...
timeout /t 1 >nul
set "GAME_DIR=D:\SteamLibrary\steamapps\common\Animal Company"
if exist "%GAME_DIR%\EACLauncher.exe" (
	start "" "%GAME_DIR%\EACLauncher.exe"
) else (
	if exist "%GAME_DIR%\AnimalCompany.exe" (
		start "" "%GAME_DIR%\AnimalCompany.exe"
	) else (
		start "" explorer "%GAME_DIR%"
	)
)
goto menu

:StopAnimalCompany
timeout /t 1 >nul
echo Stopping Animal Company...
set "GAME_DIR=D:\SteamLibrary\steamapps\common\Animal Company"

tasklist /FI "IMAGENAME eq EACLauncher.exe" | find /I "EACLauncher.exe" >nul
if %ERRORLEVEL%==0 (
	taskkill /IM EACLauncher.exe /F >nul 2>&1
	echo Killed EACLauncher.exe
) else (
	echo EACLauncher.exe not running.
)

tasklist /FI "IMAGENAME eq AnimalCompany.exe" | find /I "AnimalCompany.exe" >nul
if %ERRORLEVEL%==0 (
	taskkill /IM AnimalCompany.exe /F >nul 2>&1
	echo Killed AnimalCompany.exe
) else (
	echo AnimalCompany.exe not running.
)

rem also try to close common launcher processes (optional)
tasklist /FI "IMAGENAME eq frida.exe" | find /I "frida.exe" >nul
if %ERRORLEVEL%==0 (
	taskkill /IM frida.exe /F >nul 2>&1
	echo Killed frida.exe
)

pause
goto menu

:OpenSteamVR
echo Launching SteamVR...
timeout /t 1 >nul
set "STEAM_VR_URL=steam://run/250820"
if exist "%ProgramFiles(x86)%\Steam\steamapps\common\SteamVR\bin\win64\vrmonitor.exe" (
	start "" "%ProgramFiles(x86)%\Steam\steamapps\common\SteamVR\bin\win64\vrmonitor.exe"
) else if exist "%ProgramFiles%\Steam\steamapps\common\SteamVR\bin\win64\vrmonitor.exe" (
	start "" "%ProgramFiles%\Steam\steamapps\common\SteamVR\bin\win64\vrmonitor.exe"
) else (
	start "" "%STEAM_VR_URL%"
)
goto menu

:StopSteamVR
echo Stopping SteamVR...
timeout /t 1 >nul

tasklist /FI "IMAGENAME eq vrmonitor.exe" | find /I "vrmonitor.exe" >nul
if %ERRORLEVEL%==0 (
	taskkill /IM vrmonitor.exe /F >nul 2>&1
	echo Killed vrmonitor.exe
) else (
	echo vrmonitor.exe not running.
)

tasklist /FI "IMAGENAME eq vrserver.exe" | find /I "vrserver.exe" >nul
if %ERRORLEVEL%==0 (
	taskkill /IM vrserver.exe /F >nul 2>&1
	echo Killed vrserver.exe
) else (
	echo vrserver.exe not running.
)

tasklist /FI "IMAGENAME eq vrcompositor.exe" | find /I "vrcompositor.exe" >nul
if %ERRORLEVEL%==0 (
	taskkill /IM vrcompositor.exe /F >nul 2>&1
	echo Killed vrcompositor.exe
) else (
	echo vrcompositor.exe not running.
)
pause
goto menu

:Update Logs
timeout /t 1 >nul
echo opening update logs...
timeout /t 2 >nul
echo =====================================================
echo      \\This text is dumped by Nova menu//
echo                   \\Menu//
echo                   Fix menu.
echo               Better gui F0R cmd.
echo                \\added mods//
echo            Black Backpack spawner.
echo                revolver spawner.
echo               tripwire spawner.
echo                RPG Ammo spawner.
echo                 Crate spawner.
echo				New tuff themes.
echo                   \\Bugs//
echo       the new theme doesnt show the gun lib .
echo                                 
pause
goto menu

:credits
cls
echo ==========================
echo         CREDITS
echo ==========================
echo.
echo Nova Launcher
echo Created by: XXFCAT
echo UI Designed in CMD
echo.

pause
goto menu

:settings
cls
echo ==========================
echo        SETTINGS
echo ==========================
echo.
echo 1. Purple Theme
echo 2. Blue Theme
echo 3. Green Theme
echo 4. Aqua Theme
echo 5. Red Theme
echo 6. Purple Theme
echo 7. Yellow Theme
echo 8. White Theme
echo 9. Gray Theme
echo 10. Light Blue Theme
echo 11. Light Green Theme
echo 12. Light Aqua Theme
echo 13. Light Red Theme
echo 14. Light Purple Theme
echo 15. Light Yellow Theme
echo 16. Bright White Theme
echo 17. Back to Menu
echo.
set /p theme=Choose:

if "%theme%"=="1" color 00
if "%theme%"=="2" color 01
if "%theme%"=="3" color 02
if "%theme%"=="4" color 03
if "%theme%"=="5" color 04
if "%theme%"=="6" color 05
if "%theme%"=="7" color 06
if "%theme%"=="8" color 07
if "%theme%"=="9" color 08
if "%theme%"=="10" color 09
if "%theme%"=="11" color 0A
if "%theme%"=="12" color 0B
if "%theme%"=="13" color 0C
if "%theme%"=="14" color 0D
if "%theme%"=="15" color 0E
if "%theme%"=="16" color 0F
if "%theme%"=="17" goto menu

pause
goto settings

:exit
cls
echo Thanks for using Nova Launcher!
timeout /t 3 >nul
exit

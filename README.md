# winerun

	winerun -- wine cmdline tool
	version 1.3

	* no need to set WINEPREFIX or "cd" into the right folder
	* easy version management
	* auto-restores screen-size if changed within wine 
	* intuitive, small and fast

	syntax:
	    winerun [gdb|dbg|dryrun|copy] [[version] <wineversion>|wine|lutris>] [prefix] <wineprefix>|<exe> [new] [cd] [[exec] <exe>|<shellscript>] [<args>]
	    winerun [gdb|dbg|dryrun] [[version] <wineversion>]|wine|lutris>] [prefix] <wineprefix>|<exe> [cd] [winecfg|regedit|msiexec|regsvr32|reg|cmd|winetricks|noteapad] [<args>]
	    winerun [dryrun] [prefix] <wineprefix>|<exe> [edit|firefox|gimp|kill|suspend|resume] <args>
	    <exe name> [gdb|dbg|dryrun] [[version] <wineversion>|wine|lutris>] [[exec <exe>|<shellscript>]|winecfg|regedit|msiexec|regsvr32|reg|cmd|winetricks|noteapad|edit|firefox|gimp] [<args>]

	with:
	    - <wineprefix>: either a full path or defined in WINEDRIVES
	    - <exe>: a full or partitional path with shell patterns (*?) with or without ".exe" extensions
	    - <exe name>: renamed/liked winerun with the filename of any *.exe inside of a prefix  with or without ".exe" extensions
	    - copy: copies the winrun script to <prefix>/<exe without path> to be started with that script by calling it directly or symolic linking it
	    - copy additonal creates <prefix>/<exe without path>.desktop file (does not overwrite existing file) 
	    - if both wrestool (icoutils) and convert (ImageMagic) are installed copy creates an <exe>.png iconfile from the windows icon (no overwrite)
	    - can be killed, resumed or suspended - kill can have a different signal than default 9 as argument
	    - <shellscript>: a full or partitional path with shell patterns with ".sh" extensions
	    - <wineversion>: either a folder defined in WINERUNNERS or a number used as pattern in the same WINERUNNERS folders
	    - cd: changes dir to the same folder the <exe> is found or to <prefix>/drive_c if no <exe> is given
	    - new: creates new prefix (in the first WINEDRIVES folder if no absolute path is given)
	    - dpg / gdb use internal or gdb as debugger
	    - dryrun: do not execute or create anything (apart from .sh scripts in <prefix>) but print-out the actions
	    - also "wine" or "lutris" can be used for version: it removes any saved version and default to either system wine or the lutris version defined in .yml
	    - when "exec" is not used then "cd" is assumed
	    - all exept <prefix> ignore case distinction 
	    - if only prefix is given then it will try to find the exe and path from a Lutris .yml configuration
	    - in most places "find" is used to find the file if no absolute path is given
	    - will not follow linked folders
	    - if more then one alternative is found then the command will be interupted and the alternatives printed on screen

	examples:
	    winerun GRunner
	    winerun GRunner kill
	    winerun 4.24 grunner -fullscreen y
	    winerun version 4.24 prefix WGame cd exec grunner.exe -fullscreen y -playnet 2
	    winerun wine ~/WPrefixes/WGame new exec /media/user1/CD1/Setup.exe
	    winerun Grun* notepad readme.txt
	    winerun version lutris-4.21-x86_64 WGame Bin/Release/GRunner
	    winerun GRunner.exe edit gfx.ini
	    winerun dryrun GRunner.exe regedit myconfig.reg
	    winerun lutris WGame exec lvlEdit 
	    winerun WGame gimp image/sell0.png
	    winerun copy 4.24 GRun* -fullscreen y
	    ./WGame/GRunner -playnet 2
	
	env vars:       (auto-assigned)
	    WINEDRIVES  (/files/Games)
	    WINERUNNERS (/files/wine)
	    WINE        (wine)
	    WINEEDITOR  (/usr/bin/mcedit)

	<prefix>/winerun.sh file:
	    - will contain the last WINE=<version>
	    - can also contain any user-defined script like "export WINEDEBUG=+loaddll"
	    - will be removed when empty
	    - can use relative path for wine binary with <prefix> as start (to use as bottle)

	<prefix>/<exe name without .exe>.sh file:
	    - shellscript will be sourced before running exe with the same name
	    - autoupdates with options="<cmdline options>" when "copy" is used

	vars to be used with the above .sh scripts:
	    noscreen_restore=1 (disables the auto restore screensize feature)
	    options="<args to exe>" (will by prefixed to cmdline args)

	<prefix>/<exe name without .exe>.lua file:
	    - will call lua with the script and the wine exe call as arguments
	    - non zero exit status will stop winerun
	    - will be ignored while dryrun 

	linked/renamed winerun:
	    - linked/renamed winerun will run winerun with <filename> as <exe> 
	    - renamed copy of winerun in a WINEPREFIX will be used as <exe> inside of the prefix (can be created with: 'winerun copy' )
	    - above copy can be symbolical linked (link name can be anything)


    

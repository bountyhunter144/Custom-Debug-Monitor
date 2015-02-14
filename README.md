Custom Debug Monitor
============


This is a debug menu I have created and I figured it would be of use to some of you so here it is.


# Table of Contents:
* [Epoch 1.0.5.1](https://github.com/noxsicarius/Custom-Debug-Monitor/tree/1.0.5.1#for-epoch-1051)
* [Epoch 1.0.4.2a](https://github.com/noxsicarius/Custom-Debug-Monitor/tree/1.0.4.2#for-epoch-1042a)


# For Epoch 1.0.4.2a


![Debug Monitor](https://scontent-b-atl.xx.fbcdn.net/hphotos-xpf1/v/t1.0-9/10492282_780169578712954_6075501529329797732_n.jpg?oh=4ac1f02e919557a4bbe02289bad85d65&oe=5502DD57)


1. Click ***[Download Zip](https://github.com/noxsicarius/Custom-Debug-Monitor/archive/1.0.4.2.zip)*** on the right sidebar of this Github page.

	> Recommended PBO tool for all "pack", "repack", or "unpack" steps: ***[PBO Manager](http://www.armaholic.com/page.php?id=16369)***

1. Log into your server via FTP or your host's File Manager. Locate, download, and unpack your ***MPMissions/Your_Mission.pbo***, and open the resulting folder.
 
	> Note: "Your_Mission.pbo" is a placeholder name. Your mission might be called "DayZ_Epoch_11.Chernarus", "DayZ_Epoch_13.Tavi", or "dayz_mission" depending on hosting and chosen map.

1. Extract the downloaded folder.

1. If you do not have a custom compiles.sqf do step (A). If you have a custom compiles.sqf do step (B).
	   
	> #### (A)

	> 1. Navigate to your mission folder and open the ***init.sqf***.

	> 1. Find this line:

	> 	~~~~java
	> 	call compile preprocessFileLineNumbers "\z\addons\dayz_code\init\compiles.sqf";
	> 	~~~~
	> 	And replace it with this:
	> 	~~~~java
	> 	call compile preprocessFileLineNumbers "custom\compiles.sqf";
	> 	~~~~

	> 1. Copy the ***custom folder*** (in the download) into your mission folder.
	
	> #### (B)

	> 1. Open your custom ***compiles.sqf*** and replace this line:

	> 	~~~~java
	>	dayz_spaceInterrupt =			compile preprocessFileLineNumbers "\z\addons\dayz_code\actions\dayz_spaceInterrupt.sqf";
	> 	~~~~
	> With this line:
	> 	~~~~java
	>	dayz_spaceInterrupt =			compile preprocessFileLineNumbers "custom\dayz_spaceInterrupt.sqf";
	> 	~~~~
	
	> 	Note: If you do not already have this line in your compiles then simply add the new line to your custom compiles.
	
	> 1. Copy the contents of the ***custom folder*** (in the download) into your custom folder ***except for the compiles.sqf***.
	
1. Open the ***init.sqf*** in the root of your mission folder and paste the following at the bottom of the if(!isDedicated) code:

	~~~~java
	if (isNil 'debugMonitor') then 
	{
		debugMonitor = true;
		_nill = execvm "custom\debug_monitor.sqf";
	};
	~~~~

	It should now look like this:
	
	~~~~java
	if (!isDedicated) then {
		
		
		**Some code found here**
		
		
		if (isNil 'debugMonitor') then 
		{
			debugMonitor = true;
			_nill = execvm "custom\debug_monitor.sqf";
		};
	};
	~~~~
	
1. If you use snap build pro replace the space interrupt file ***[with this one](https://github.com/noxsicarius/SnapPro/blob/debug-compatible/custom/snap_pro/dayz_spaceInterrupt.sqf)***
1. Package the PBO and send it to the server. Everything is finished.

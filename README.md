# Autofix for AMD 5xxx cpus sometimes running at less than 1 GHZ

**If you only want to see how to fix the problem go straight to** [Automating the fix.](#automating-the-fix)
**Be sure to read the** [Disclaimer.](#disclaimer)

## The problem:
I found out about this after upgrading the CPU from a Ryzen 5 2600 to a Ryzen 5 5600x on an Asrock B450 pro4.
After properly installing it and turning on the computer, The pc was lagging like hell and after some minutes I found the issue: **the cpu was running at 0,67 ghz without a reason**. 
I don't know what causes this behaviour. 
At first I thought that the cpu was faulty so I sent it back and got a replacement only to find out it wasn't a cpu problem.

## The fix:
After googling from some time, I found out you could fix this issue by disabling PROCHOT from ryzen master.
This process does the job, but turning on a pc then having to open ryzen master and disabling PROCHOT from it with a 0,67 ghz cpu is not exactly fast but it seems that you can't make ryzen master apply those settings at startup.

## Fix v2:
After doing this process for some months, I was really sick of it.
So I thought "isn't there a way to use ryzen master from command line?". Turns out there's a way.
Thanks to [this thread](https://www.reddit.com/r/Amd/comments/qn8o7n/hidden_command_line_version_of_ryzen_master_found/), I discovered that asrock motherboard utility installation comes out with an integrated ryzen master command line interface tool. From here it was really easy to create a batch file that calls the command to disable PROCHOT at startup by scheduling it on the task scheduler (it seems that just putting the .bat in the startup folder does not work.).

## Automating the fix:

 1. Download and install Asrock motherboard utility, doesn't matter if you don't have one as we only need the executable that let's you run ryzen master services from CLI. I used ver:3.0.466, [here's the link.](https://download.asrock.com/Utility/MotherboardUtility/MotherboardUtility%28v3.0.466%29.zip)
 2. After installing it, you have to create a .bat file with the command to disable PROCHOT. 
     In order to do this, you just need to paste this in a text file:
	  `"PATH\OF\INSTALLATION\ASRock Utility\A-Tuning\Bin\AMDRMCLI.exe" -a DisablePROCHOT`.
	  And save it with whatever name you want but make sure it has `.bat` as its extension.
	  Place it in a comfy location as it will have to stay there and never be touched again.
3. Now open the start menu, look for the **task scheduler** and open it.
4. Now create a task and fill the sections as shown below:![General](https://i.imgur.com/zU84bLC.png)

	![triggers](https://i.imgur.com/aaLl0mm.png)
	![Actions](https://i.imgur.com/75LcQET.png)
	![Conditions](https://i.imgur.com/M3c1ixH.png)
	![Settings](https://i.imgur.com/3bvFEUN.png)
5. Press `OK` and save it. That should be all. 
## Contributing
Even if this process does the job, I know it can be refined.
Feel free to make pull requests or your own repo. (thanks are welcome if this process helped you make your own version of the fix :D).
 Any pull requests with useful corrections or process refinment will be accepted.
## License
Not sure if I need to specify that but any contribution and this process are under MIT license.
# DISCLAIMER
There should be no issues with using your computer with disabled prochot but since it is a measure to prevent cpu from damaging itself from overheating, I take no responsability of what you are going to do after disabling it and about any damage that is caused to any of your components that can be reconduced to this procedure. 
If you fear damaging your components, do not follow it. 
There should be no problems if you enable PROCHOT after the task disables it anyway.

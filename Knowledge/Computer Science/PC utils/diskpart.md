**Format a USB flash disk using DiskPart on Windows 11**

1. Plug in the USB drive.
    
2. Open **Command Prompt as Administrator**.
    
3. Run:


	```Cmd
	diskpart 
	list disk 
	select disk=X (replace X with your USB disk number) 
	clean 
	create partition primary 
	format fs=fat32 quick (or ntfs / exfat)
	assign
	exit
	```

⚠️ **Warning:** Selecting the wrong disk will erase it completely.
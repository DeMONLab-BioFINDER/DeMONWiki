# How to connect to Taotie

Connect to the zte-router either through the wireless network or plug in the ethernet cable from the LAN port. 

If the machine is on you should now be able to see it among your network drives. 

If you try to enter the drive you will be prompted for a username and password. This information is stored in the office [decide somewhere to store it].

With correct user and pass you can now access drive. 

If you prefer a graphical interface then enter Taotie's IP address in a browser. The address may change but for me it was 192.168.5.3 [should maybe assign a static IP?]. 

The graphical interface is fine for uploading or downloading smaller files. But for bigger transfers you want to user rsync and then have to mount the shared folder "Datasets". 
```
mount -t cifs -o user=TaotieAdmin,uid=1000,gid=1000,vers=3.0 //taotie.local/datasets ~/mount_folder
```
You will be prompted to supply a password and when that is done you can use rsync as usual, eg:

```
rsync -auh --info=progress2  /path_to_your_data /mount_folder

```
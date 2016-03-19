 
##What is clat? 

This repository is called after *clat*. A bash script that allows, via transmission-remote, distributing your torrent downloaded series in folders. If you don't use [Transmission](https://www.transmissionbt.com/) for your torrents, you can still use the second script, named *aseries*. This one doesn't manage torrent but just files and works with the same structure of clat. Actually, I wrote aseries first. But when aseries moved my tv series and shows to their particular folder, their torrents stopped working. I queried the web and found it was possible to alter torrents with *transmission-remote*. Before you go crazy I'll explain my home LAN scheme. I have a Network Attached Server (NAS) running Transmission. I manage all the torrents stuff through it using Transmission Remote GUI on my main PC. Which is a graphical user interface for transmission-remote. I find this layout very convenient because my NAS can keep downloading files and sharing them with others while my main computer is off. Anyway, this is not to sell NAS systems. If you don't have a NAS, you can mount your server on an old PC with GNU/Linux. I have a friend that uses an old NetBook for this matter. If you don't want a server at all, You can run Transmission on your main computer and use transmission-remote with localhost address. So the only prerequisite is to have a copy of Transmission running somewhere and configured with remote access. And then our little transmission-remote command (in case you want to install it, the pack is called transmission-cli).


##Getting started

Before all, download a copy of clat and copy the file to ~/bin/ or any other folder that you know is on the PATH environment variable.

Before opening it with your favourite text editor, you need to create some information structure. For every tv series or show you want to separate to a different location on your filesystem, clat needs you to create a file whose name is the series' name and whose content is the path to the folder where you want clat to move that series. For instance, if you have a series called XYZ, here's how you have to set your file:

```
  echo "/share/HDB_DATA/Downloads/transmission/complete/series/XZY/" > XZY
```

>The file name is case sensitive because it has to be compared with your download's files to see if a file is from such a series. The path is also case sensitive on some Operating Systems. Be aware of that.

>Notice that the path you need belongs to whatever filesystem your Transmission is running onto. Perhaps you are used to reach your files from here: ...~/NAS/transmission/completed/.... That is because the server has some shared folders and you can mount them in any point of your filesystem. Remember we are asking Transmission to move the file and update the torrent, so the path has to be relative to Transmission filesystem. I mean, if you have a server running Transmission, the path belongs to your server. If you don't know it, this command can help:

```
transmission-remote server-ip:port --auth user:pass --torrent 1 --info | grep "Location:"
```

>If that command doesn't show you anything, perhaps the torrent id 1 just doesn't exist. Try with other number. You can also see the torrent list with their ids:

```
transmission-remote server-ip:port --auth user:pass -l
```

This kind of files are like pointers and tell clat the series and the location you want the files of that series to be moved. Clat queries a folder to reach that kind of pointer files. So you need to have all of them on the same folder. This time, the folder has to be on your main computer's filesystem. Where to put the folder, you chose. All you have to do is modify the DIR variable inside the script to the path of your choice. You can have as many pointer files as you may need. But make sure there are no other files unrelated to clat in that very folder.

Now all it's left to be done is modifying the SERVER variable. You have to tell clat your server IP, the Transmission's port and, after "--auth " the pair of user and password you have set on Transmission config (remote tab). If you choose not to put user and password, you can remove the "--auth " part. If you run Transmission on your main PC together with transmission-remote, the SERVER variable could look like this:

```
SERVER="localhost:9091"
```

But if Transmission runs in a server in your local network, which static IP is 192.168.1.5, and you have ser a user and a password. Then it could look like this:

```
SERVER="192.168.1.5:9091 --auth ian:passwd1"
```

>Remember to look at the port on your config and to change it accordingly.

##What is aseries
I still haven't refined it. For instance, there are no config variables and you have to modify the code directly to make it work. It is not a difficult task though.

I'll add some more information after I improve the code making some more readable.

# The Defenitive Guide to Updating Garuda Linux via Pacman in Iran inspite of the Internet Blockages (No VPNs &amp; 100% Free) [Tested & Still Working in 2023/Jan/18]

### In this guide, I'll be hopefully helping you (My Iranian Friend) to either Update or to Install Apps/ Packages on your Garuda Linux Installation with noting more than a few edits to a  few files & installation fo 2 packages via their respective .tar.zst files, So Let's Get started! 

## Step1:
#### Go to the following Directory <code>etc/pacman.d/</code> & make sure to backup (Just copy to your desktop) the two files named <code>Mirrorlist</code> & <code>Chaotic-MirrorList</code> as we'll be making edits in them!

## Step2: 
#### Open up the original <code>Mirrorlist</code> file located in <code>etc/pacman.d/Mirrorlist</code> and change the text inside to: (Delete all the text inside and copy this there!)
```
Server = https://mirror.hostiran.ir/archlinux/$repo/os/$arch
Server = http://mirror.hostiran.ir/archlinux/$repo/os/$arch
```

## Step3:
#### Now, Open up the original <code>Chaotic-MirrorList</code> file located in <code>etc/pacman.d/Chaotic-Mirrorlist</code> and change the text inside to:  (Delete all the text inside and copy this there!)

```
# CloudFlare
Server = https://chaoticmirror.com/chaotic-aur/$repo/$arch
```

##### *Now, technically speaking, Pacman should be able to downlaod all the Databases, however, due to the Deep-Packet-Inspection used by the blockages, this is impossible as a TLS handshake cannot be done with some servers! Inorder to bypass this, we'll be switching the Pacman Downloading Engine from Wget to Aria2c in order to disable the TLS requirements! Here's how to do this:

## Step4: 
#### Download these two files via Firedragon into the <code>Downlaods</code> folder of your PC (official repo files that Pacman cannot downlaod, but Firedragon can!):
```
https://mirror.hostiran.ir/archlinux/extra/os/x86_64/c-ares-1.18.1-1-x86_64.pkg.tar.zst
https://mirror.hostiran.ir/archlinux/community/os/x86_64/aria2-1.36.0-1-x86_64.pkg.tar.zst
```

## Step5: 
#### Now open up Konsole and run in order from top to bottom:
```
sudo pacman -U /home/garuda/Downloads/c-ares-1.18.1-1-x86_64.pkg.tar.zst
sudo pacman -U /home/garuda/Downloads/aria2-1.36.0-1-x86_64.pkg.tar.zst
```

#### As a final step, we'll be changing the Pacman downlaoder to Aria2c, and in order to do that, we must edit the <code>pacman.conf</code> file located in the <code>/etc</code> folder of our installation!

## Step6: 
#### Open <code>/etc/Pacman.conf</code> (not pamac.conf, that's a whole different thing!), and add the following text just under the <code>[Options]</code> name:
```
XferCommand = /usr/bin/aria2c --allow-overwrite=true --continue=true --file-allocation=none --log-level=error --max-tries=2 --max-connection-per-server=2 --max-file-not-found=5 --min-split-size=5M --no-conf --remote-time=true --summary-interval=60 --timeout=5 --dir=/ --out %o %u
```

#### & we're finally done! Now, you can easily run <code>sudo pacman -Syy</code> to update your databases, and even tho the Aria2c UI is much worse that the Wget one in Konsole, it still gets the job domne better than anything else!

## If you'de like to support me, plz consider donating to my Crypto wallet at: 
```
BTC: bc1q235ljppmkc3sly0z4vkwmame9l6ttnstkmqmel
```

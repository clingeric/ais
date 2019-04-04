# ais
AIS SCLC 2019: Intro To Ethical Hacking Workshop

*[view presentation](https://docs.google.com/presentation/d/11q5NdueYcfb-YIdiU8_EaT2s7srxvopdatAkMK9p4wY/edit?usp=sharing)*

## 0
*Required Downloads*
* [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
* [Kali Linux](https://www.offensive-security.com/kali-linux-vm-vmware-virtualbox-image-download/) (*available for VirtualBox and VMWare*)

## 1
*Install Kali Linux*

In VirtualBox, go to “File” > “Import Appliance”, then browse to the `.ova` file downloaded in the previous step.

After the virtual machine imports, select the Kali VM and click the settings icon:

Under the system pane, set these Memory” to 8192 MB if you have 12 or more gigabytes of RAM on your laptop. If you have 8 GB of RAM on your laptop, set the “Base memory” to 4096 MB.

Boot up Kali and log in

Username: `root`
Password: `toor`

You can now delete the “.ova” file if you’re low on disk space.

Assure you have the RockYou password list

```shell
cd /usr/share/wordlists
```

You should see `rockyou.txt`

If you see `rockyou.txt.gz`, unzip it first with `gunzip rockyou.txt.gz`

## 2 
*Password Cracking with Hashcat*

Return to the home directory

```shell
cd
```

Download the [LinkedIn password hash list]() into your home directory

Run `hashcat` using the list of LinkedIn password hashes and the RockYou password list

```shell
hashcat --force -m 100 --potfile-disable --remove --outfile=LinkedIn_cracked.txt password_hashes.txt /usr/share/wordlists/rockyou.txt
```

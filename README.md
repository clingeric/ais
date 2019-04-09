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

Download the [LinkedIn password hash list](https://raw.githubusercontent.com/clingeric/ais/master/passwords.txt) into your home directory

Check the file to see how many password hashes there are

```shell
wc -l password_hashes.txt
```

*There should be 286*

Run `hashcat` using the list of LinkedIn password hashes and the RockYou password list

```shell
hashcat --force -m 100 --potfile-disable --remove --outfile=LinkedIn_cracked.txt password_hashes.txt /usr/share/wordlists/rockyou.txt
```

Hashcat will run for a few minutes.

Press `S` to check the progress of the cracking

It's important to note that the `hashcat` command uses the `--remove` flag to remove hashes from the hash list when it is cracked

Once done, check the number of hashes are remaining

```shell
wc -l password_hashes.txt
```

*There should be ???*

Next, open the `LinkedIn_cracked.txt` file to see the results of the password cracking

```shell
nano LinkedIn_cracked.txt
```

*The cracked password is found after the : on each line*

## 3

*SQL Injection*

## 4

*Social Engineering with the Social Engineering Toolkit (SET)*

Navigate to the `/opt/set` directory of Kali Linux

```shell
cd /opt/set
```

Run the Social Engineering Toolkit

```shell
./setoolkit
```

Select option 1 for `Social-Engineering Attacks`

Select option 2 for `Website Attack Vectors`

Select option 3 for `Credential Harvester Attack Method`

Select option 2 for `Site Cloner`

After you've selected this feature, you'll need to set an IP address to host the cloned site. Set `IP address for the POST back in Harvester/Tabnapping` to the IP address (previously configured in bridged mode of Kali Linux

Set the cloned website to `http://www.facebook.com` (enter the *full* URL including `http://`)

*When SET asks you about Apache, enable it to start the webserver.


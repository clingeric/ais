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
wc -l passwords.txt
```

*There should be 282093*

Run `hashcat` using the list of LinkedIn password hashes and the RockYou password list

```shell
hashcat --force -m 100 --potfile-disable --remove --outfile=LinkedIn_cracked.txt passwords.txt /usr/share/wordlists/rockyou.txt
```

Hashcat will run for a few minutes.

Press `S` to check the progress of the cracking

It's important to note that the `hashcat` command uses the `--remove` flag to remove hashes from the hash list when it is cracked

Once done, check the number of hashes are remaining

```shell
wc -l passwords.txt
```

*There should be 193622*

Next, open the `LinkedIn_cracked.txt` file to see the results of the password cracking

```shell
nano LinkedIn_cracked.txt
```

*The cracked password is found after the : on each line*

Let's try the same wordlist with the [best64](https://github.com/hashcat/hashcat/blob/master/rules/best64.rule) rule. This rule appends common numbers at the end of passwords and performs other simple permutations.

```shell
hashcat --force -m 100 --potfile-disable --remove --outfile=LinkedIn_cracked.txt passwords.txt -r /usr/share/hashcat/rules/best64.rule /usr/share/wordlists/rockyou.txt
```

```shell
wc -l passwords.txt
```

*There should be 144860*

## 3

*Social Engineering with the Social Engineering Toolkit (SET)*

Search for the Social Engineering Toolkit under the Kali applications list.

Run the application

Select option 1 for `Social-Engineering Attacks`

Select option 2 for `Website Attack Vectors`

Select option 3 for `Credential Harvester Attack Method`

Select option 2 for `Site Cloner`

After you've selected this feature, you'll need to set an IP address to host the cloned site. Set `IP address for the POST back in Harvester/Tabnapping` to your IP address (if you installed the image of Kali from the provided link, you should only have to hit enter).

Set the cloned website to `http://www.facebook.com` (enter the *full* URL including `http://`)

Hit enter when it asks if you know what you're doing

Open your web browser to the IP address you entered previously or `127.0.0.1`.

Enter some fake credentials into the fields.

Go back to the open Social Engineering Toolkit to see your fake credentials.

## 4
*SQL Injection*

SQLi Demo:
https://www.hacksplaining.com/exercises/sql-injection#/start

SQLi Cheat Sheet:
https://www.netsparker.com/blog/web-security/sql-injection-cheat-sheet/

SQLi Prevention Cheat Sheet 1:
https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.md

SQLi Prevention Cheat Sheet 2:
https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Query_Parameterization_Cheat_Sheet.md

## 5
*Tools to Learn*

[OWASP Zap](https://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project)

[Burpsuite](https://www.pentestgeek.com/web-applications/burp-suite-tutorial-1)

[Metasploit](https://www.offensive-security.com/metasploit-unleashed/)

[Nessus](https://sectools.org/tool/nessus/)




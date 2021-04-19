![](https://img.shields.io/github/languages/top/alexevladgabriel/fastdl-pterodactyl?label=Shell&style=flat-square)
![](https://img.shields.io/github/license/alexevladgabriel/fastdl-pterodactyl?color=F56E41&label=License&style=flat-square)
![](https://img.shields.io/badge/Discord-Scai%238477-0E47B3?style=flat-square)
# FastDownload Pterodactyl v1.X v2
Module FastDL, fork of [Dr3Amer3r](https://github.com/Dr3Ame3r/pterodactyl_fastdl) <br>Simplified version.


AppID | Game | Supported
------------ | ------------- | :--:
~ | If you test a game and see it's working contact me to add to the list | ⚠️
~ | All HL1/HL2 games and mods | ✅ 
440 | [Team Fortress 2](http://store.steampowered.com/app/440/) | ✅ 
500 | [Left 4 Dead](http://store.steampowered.com/app/500/) | ✅ 
550 | [Left 4 Dead 2](http://store.steampowered.com/app/550/) | ✅ 
730 | [Counter-Strike: Global Offensive](http://store.steampowered.com/app/730/) | ✅ 
4000 | [Garry's Mod](http://store.steampowered.com/app/4000/) | ✅ 
225840 | [Sven Coop](http://store.steampowered.com/app/225840/) | ✅

## Installation
1. Run the command below to assign user www-data to group pterodactyl
  * ``` gpasswd -a www-data pterodactyl ```
2. Run the commands below to set group permissions for read and exec
  * ``` chmod 755 /var/lib/pterodactyl/ && chmod 755 /var/lib/pterodactyl/volumes/ ```
3. Add the command below in the last line of Eggs "Install script"
  * ``` chmod 750 /mnt/server/ ```


## NGINX Configuration

 1. Add current virtual.conf to conf.d directory of a nginx daemon and edit the line, ith your currently running node **FQDN**.
  This virtual.conf is configured to run as root under /var/lib/pterodactyl/volumes/ and list directories from here as default.
  
 *  ``` server_name  example.website.ro; ```
  
## Pterodactyl Panel
1. We will need to configure our egg to use a JSON file parser.

```
{
    "csgo/cfg/server.cfg": {
        "parser": "file",
        "find": {
            "sv_downloadurl": "sv_downloadurl \"http://{{env.P_SERVER_LOCATION}}/{{env.P_SERVER_UUID}}/csgo/\"",
            "sv_allowdownload": "sv_allowdownload \"1\"",
            "sv_allowupload": "sv_allowupload \"0\""
        }
    }
}
```

**NOTE**: Please pay attention that the "sv_downloadurl" variable has a /csgo at the end, this can be configured on ANY running egg with your desired path.


![alt text](http://repository.btstelecom.ro/pterodactyl_images/Screenshot_15.png)

After that, we need to name our locations as our **FQDN** (this was much easier for me to configure it as we have the description for locations who show our CPU names.
So, location list should contain in "Short Code" the FQDN address, let's say 'example.website.ro' or your domain.
Finally, restart your nginx and your server running with the edited egg. That's it.

* ``` systemctl restart nginx``` or ```nginx -s reload```

Our **sv_downloadurl** will be like this
`http://example.website.ro/{{PTERODACTYL_UUID}}/csgo`

## Credits:
Dr3Amer3r - [Pterodactyl FastDL Version v1](https://github.com/Dr3Ame3r/pterodactyl_fastdl)

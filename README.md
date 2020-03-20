Note - this guide assumes a Debian-based distro such as Ubuntu. I'll leave it as an exercise for the reader to adapt this for non-Debian-based distros.

1. Drop both unit files in /usr/lib/systemd/system
2. Create a service account for Minecraft: `adduser --system --home /opt/minecraft --group --disabled-password minecraft`
3. Download the minecraft server jar. Rename it to `minecraft_server.1.15.2.jar` (or whatever version you choose), and stick it in /opt/minecraft
4. Create a symlink from `/opt/minecraft/minecraft_server.latest.jar` to `/opt/minecraft/minecraft_server.1.15.2.jar`. (This indirection allows trivial upgrades later by just changing symlinks.)


5. Decide on a "server" name. This should be a single word ideally - I'm gonna use "gloom", because that happens to be the hostname of the box it's running on. It should be meaningful to you, and distinct from other minecraft servers on the box. Anywhere you see the word "gloom" in the remainder of these instructions, substitute in your chosen word.
6. `sudo -u minecraft mkdir -p /opt/minecraft/gloom`
7. `echo eula=true > /opt/minecraft/gloom/eula.txt`
8. `ln -s /opt/minecraft/minecraft_server.latest.jar /opt/minecraft/gloom/minecraft_server.jar`
9. `sudo systemctl enable minecraft@gloom.service`
9. `sudo systemctl start minecraft@gloom.service`

That's it! You can write to the server console by writing to `/run/minecraft-gloom.control` - for example `echo 'op stwalkerster' >> /run/minecraft-gloom.control`.

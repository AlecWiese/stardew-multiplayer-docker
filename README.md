# Stardew Valley Multiplayer Docker Compose

This project aims to autostart a Stardew Valley Multiplayer Server for version 1.6 and SMAPI 4.0.0, as easy as possible. It's very much still a work in progress.

## Side Note

 - Updating to most recent version requires a rebuild: `docker-compose build --no-cache` 
 - I barely know what I'm doing. maybe see if there's a better fork first?
 - Thanks to printfuck and jolekay for their work

## Setup

### Docker-Compose
 
Again, I'd like to stress it would be better for your sanity to find another source

```
git clone https://https://github.com/AlecWiese/stardew-multiplayer-docker

docker-compose up
```

## Game Setup

Intially you have to create or load a game once via VNC or Web interface. After that the Autoload Mod jumps into the previously loaded savegame everytime you restart or rebuild the container. The AutoLoad Mod config file is by default mounted as a volume, since it keeps the state of the ongoing SaveGame, but you can also copy your existing SaveGame to the `Saves` volume and define the SaveGame's name in the environment variables.

### VNC

Use a vnc client like `TightVNC` on Windows or plain `vncviewer` on any Linux distribution to connect to the server. You can modify the VNC Port and IP address and Password in the `docker-compose.yml` file like this:

Localhost:
```
   # Server is only reachable on localhost on port 2342...
   ports:
     - 127.0.0.1:2342:5900
   # ... with the password "insecure"
   environment:
     - VNCPASS=insecure
```

### Web Interface 

On port 5800 inside the container is a web interface. This is a bit easier and more accessible than just the VNC interface. Although you will be asked for the vnc password, I wouldn't recommend exposing the port to the outside world.

![img](https://store.eris.cc/uploads/859865e1ab5b23fb223923d9a7e4806b.PNG)

## How it works

The game will be pulled from my servers (I'll assume you already own the game - since you're looking for a multiplayer - so please don't rip it from there) and the modloader (SMAPI) will be pulled from Github when building the container. You can control the mods's settings with environment variables in the `docker-compose.yml` file.

## Used Mods

* [AutoLoadGame](https://www.nexusmods.com/stardewvalley/mods/2509)
* [Always On](https://community.playstarbound.com/threads/updating-mods-for-stardew-valley-1-4.156000/page-20#post-3353880)
* [Unlimited Players](https://www.nexusmods.com/stardewvalley/mods/2213)
* some more ...

## Troubleshooting

### Error Messages in Console

Usually you should be able to ignore any message there. If the game doesn't start or any errors appear, you should look for messages like "cannot open display", which would most likely indicate permission errors.

### VNC

Access the game via VNC to initially load or start a pregenerated savegame. You can control the Server from there or edit the config.json files in the configs folder.

### Performance

I'd recomend a VPS/Machine with at least four logical CPUs and 4GB Ram, otherwise there will be horrible lags. The minimum configuration I'd consider playable with two to four players would be two logical CPUs and 1GB of Ram.

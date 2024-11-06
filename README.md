<div align="center" style="background-color: #111; padding: 100;">
    <a href="https://github.com/davidclaeysquinones/Threadfin"><img width="285" height="80" src="html/img/threadfin.png" alt="Threadfin" /></a>
</div>
<br>

# Threadfin
## M3U Proxy for Plex DVR and Emby/Jellyfin Live TV. Based on xTeVe.

This repository is a fork of the [original](https://github.com/Threadfin/Threadfin).
To be honest I'm not sure where I'll be able to take this proyect but let's say I'll take it as a learning opportunity.
The reason I decided to fork the code is that I don't like the direction the proyect is headed.
If at some point I feel like I've reached something with this repo I might consider a rename for this fork (feel free to propose names).

If you have some experience with Go help is more than welcome. If there are feature requests you would like feel free to ask.


Old xTeVe documentation for setup and configuration can be found [here](https://github.com/xteve-project/xTeVe-Documentation/blob/master/en/configuration.md).

## Roadmap

* try to fix m3u filtering for larger playlists

## Requirements
### Plex
* Plex Media Server (1.11.1.4730 or newer)
* Plex Client with DVR support
* Plex Pass

### Emby
* Emby Server (3.5.3.0 or newer)
* Emby Client with Live-TV support
* Emby Premiere

### Jellyfin
* Jellyfin Server (10.7.1 or newer)
* Jellyfin Client with Live-TV support

--- 

## Threadfin Features

* New Bootstrap based UI
* RAM based buffer instead of File based

#### Filter Group
* Can now add a starting channel number for the filter group

#### Map Editor
* Can now multi select Bulk Edit by holding shift
* Now has a separate table for inactive channels
* Can add 3 backup channels for an active channel (backup channels do NOT have to be active)
* Alpha Numeric sorting now sorts correctly
* Can now add a starting channel number for Bulk Edit to renumber multiple channels at a time
* PPV channels can now map the channel name to an EPG
* Removed old Threadfin buffer option, since FFMPEG/VLC will always be a better solution

## xTeVe Features

#### Files
* Merge external M3U files
* Merge external XMLTV files
* Automatic M3U and XMLTV update
* M3U and XMLTV export

#### Channel management
* Filtering streams
* Channel mapping
* Channel order
* Channel logos
* Channel categories

#### Streaming
* Buffer with HLS / M3U8 support
* Re-streaming
* Number of tuners adjustable
* Compatible with Plex / Emby / Jellyfin EPG

---

## Docker Image
[Threadfin](https://hub.docker.com/r/fyb3roptik/threadfin)


When I feel like I've reached something meaningfull I'll publish an image for this repository.
For now I'll refer to the original image.

* Docker compose example

```
version: "2.3"
services:
  threadfin:
    image: fyb3roptik/threadfin
    container_name: threadfin
    ports:
      - 34400:34400
    environment:
      - PUID=1001
      - PGID=1001
      - TZ=America/Los_Angeles
    volumes:
      - ./data/conf:/home/threadfin/conf
      - ./data/temp:/tmp/threadfin:rw
    restart: unless-stopped
```

---

### Threadfin Beta branch
New features and bug fixes are only available in beta branch. Only after successful testing are they are merged into the main branch.

**It is not recommended to use the beta version in a production system.**  

With the command line argument `branch` the Git Branch can be changed. Threadfin must be started via the terminal.  

#### Switch from master to beta branch:
```
threadfin -branch beta

...
[Threadfin] GitHub:                https://github.com/davidclaeysquinones/Threadfin
[Threadfin] Git Branch:            beta [Threadfin]
...
```

#### Switch from beta to master branch:
```
threadfin -branch main

...
[Threadfin] GitHub:                https://github.com/davidclaeysquinones/Threadfin
[Threadfin] Git Branch:            main [Threadfin]
...
```

When the branch is changed, an update is only performed if there is a new version and the update function is activated in the settings.  

---

## Build from source code [Go / Golang]

#### Requirements
* [Go](https://golang.org) (go1.18 or newer)

#### Dependencies
* [go-ssdp](https://github.com/koron/go-ssdp)
* [websocket](https://github.com/gorilla/websocket)
* [osext](https://github.com/kardianos/osext)
* [avfs](https://github.com/avfs/avfs)

#### Build
1. Download source code
2. Install dependencies
```
go mod tidy && go mod vendor
```
3. Build Threadfin
```
go build threadfin.go
```

4. Update web files (optional)

If TypeScript files were changed, run:

```sh
tsc -p ./ts/tsconfig.json
```

Then, to embed updated JavaScript files into the source code (src/webUI.go), run it in development mode at least once:

```sh
go build threadfin.go
threadfin -dev
```

---

## Fork without pull request :mega:
When creating a fork, the Threadfin GitHub account must be changed from the source code or the update function disabled.
Future updates of Threadfin would update your fork.

threadfin.go - Line: 29
```Go
var GitHub = GitHubStruct{Branch: "main", User: "davidclaeysquinones", Repo: "Threadfin", Update: true}

/*
  Branch: GitHub Branch
  User:   GitHub Username
  Repo:   GitHub Repository
  Update: Automatic updates from the GitHub repository [true|false]
*/

```



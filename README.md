# MiniMedia - Full Docker Compose
This repo will contain the following services to get you started
- PostgreSQL
- MiniMedia Scanner
- MiniMedia Playlist Sync
- MiniMedia MetadataAPI
- MiniMedia SonicServer
- Redis
- MusicMover

# Getting started

Clone the repo, use the openssl command to generate random hex characters (this is used for encrypting the passwords in the database)

Replace the "xxxxx" in the MiniMediaSonicServer_appsettings.json file with the random hex characters, not replacing it results in not starting the SonicServer

Replace in both json-files and docker-compose where you see "generate_password" to something more secure for the database, can be anything

Read through the docker-compose first and be concious in what it does, for example de MiniMedia Scanner will start executing all the commands which is overkill


```
git clone https://github.com/MusicMoveArr/MiniMedia-Docker-All.git
cd MiniMedia-Docker-All
openssl rand -hex 32
nano MiniMediaSonicServer_appsettings.json
```

First start postgres, give it a second before starting the rest with the second command otherwise errors will occur
```
sudo docker-compose start postgres
#wait a second before starting everything with the next command
sudo docker-compose start
```

If you're planning to use the Sonic Server, take a look in the log to get the first user (admin) password

It will show up for example as "First account is created, username: admin, password: e74314d7-b1d6-4eff-a74b-80c48ce862b6"

## Verify the Sonic Server is reachable and works

With with following we'll use curl, the result will show up empty because nothing is imported yet, but an response indicates everything is good

Replace ip address and "xxxxxxxxxxxxx" at the end of the url to the password you grabbed from the log

```
curl --location 'http://192.168.1.3:8085/rest/search3.view?u=admin&f=json&ArtistCount=100&AlbumCount=100&SongCount=100&p=xxxxxxxxxxxxx'
```

The response you can expect back in the terminal
```
{"subsonic-response":{"status":"ok","version":"1.16.1","type":"subsonic","serverVersion":"0.51.0","openSubsonic":true,"license":{"valid":true},"searchResult3":{"artist":[],"album":[],"song":[]}}}
```

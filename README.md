# Docker based media server setup

## Components

- [Jellyfin](https://jellyfin.org/) for streaming
- [Prowlarr](https://prowlarr.com/) for managing indexers
- [Sonarr](https://sonarr.tv/) for series
- [Radarr](https://radarr.video/) for movies
- [Qbittorrent](https://www.qbittorrent.org/) as a download client

## Setup

- Set the paths for storing content in the ```.env``` file
- Start the containers using

    ```
    docker-compose up -d
    ```
- Wait for the containers to start
- The respective URLs for the services are

  |Service|URL|
  |---|---|
  |Jellyfin|http://{host ip}:8096/|
  |Qbittorent|http://{host ip}:8080|
  |Radarr|http://{host ip}:7878|
  |Sonarr|http://{host ip}:8989|
  |Prowlarr|http://{host ip}:9696|
- You need to set the download client as qbittorent in both sonarr and radarr. To do this:
    - Go to Settings > Download Clients
    - Add new client
    - Set the host as the ip address of the host
    - Leave port as default (8080)
    - Test the connection and then Save
- You also need to set the root folder in both sonarr and radarr. To do this:
    - Go to Settings/Media Management
    - Click Add Root Folder
    - Browse to and select the series folder for sonarr and movies folder for radarr
- You need to add sonarr and radarr to prowlarr to automatically sync the indexers. To do this:
    - Go to Settings > Apps
    - Add new apps and select sonarr and radarr respectively
    - Set the Prowlarr Server as ```{host ip}:9696``` (Don't use localhost as it may not be accessible by sonarr and radarr)
    - Set the Sonarr and Radarr Servers as ```{host ip}:8989``` and ```{host ip}:7878``` respectively
    - Set the API key as the API key for sonarr and radarr respectively
    - You can get the API key for sonarr and radarr by going to Settings > General
    - Test the connection and then Save

## Notes

- The docker-compose file is based on the [linuxserver.io](https://www.linuxserver.io/) images
- This is only for educational purposes and I do not condone piracy in any way. Please use this only for legal purposes.

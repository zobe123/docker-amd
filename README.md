# AMD - Automated Music Downloader 

[RandomNinjaAtk/amd](https://github.com/RandomNinjaAtk/docker-amd) is a Lidarr companion script to automatically download music for Lidarr 

[![RandomNinjaAtk/amd](https://raw.githubusercontent.com/RandomNinjaAtk/unraid-templates/master/randomninjaatk/img/amd.png)](https://github.com/RandomNinjaAtk/docker-amd)

### Audio ([AMD](https://github.com/RandomNinjaAtk/docker-amd)) + Video ([AMVD](https://github.com/RandomNinjaAtk/docker-amvd)) (Plex Example)
![](https://raw.githubusercontent.com/RandomNinjaAtk/Scripts/master/images/plex-musicvideos.png)

## Features
* Downloading **Music** using online sources for use in popular applications (Plex/Kodi/Emby/Jellyfin): 
  * Searches for downloads based on Lidarr's album wanted list
  * Downloads using a third party download client automatically
  * FLAC / MP3 (320/120) Download Quality
  * Notifies Lidarr to automatically import downloaded files
  * Music is properly tagged and includes coverart before Lidarr Receives them (Third Party Download Client handles it)

## Supported Architectures

The architectures supported by this image are:

| Architecture | Tag |
| :----: | --- |
| x86-64 | latest |

## Version Tags

| Tag | Description |
| :----: | --- |
| latest | Newest release code |


## Parameters

Container images are configured using parameters passed at runtime (such as those above). These parameters are separated by a colon and indicate `<external>:<internal>` respectively. For example, `-p 8080:80` would expose port `80` from inside the container to be accessible from the host's IP on port `8080` outside the container.

| Parameter | Function |
| --- | --- |
| `-e PUID=1000` | for UserID - see below for explanation |
| `-e PGID=1000` | for GroupID - see below for explanation |
| `-v /config` | Configuration files for Lidarr. |
| `-v /downloads-amd` | Path to your download folder location. (<strong>DO NOT DELETE, this is a required path</strong>) :: <strong>!!!IMPORTANT!!!</strong> Map this exact volume mount to your Lidarr Container for everything to work properly!!! |
| `-e AUTOSTART="true"` | true = Enabled :: Runs script automatically on startup |
| `-e LidarrUrl="http://127.0.0.1:8686"` | Set domain or IP to your Lidarr instance including port. If using reverse proxy, do not use a trailing slash. Ensure you specify http/s. |
| `-e LidarrAPIkey="08d108d108d108d108d108d108d108d1"` | Lidarr API key. |
| `-e MBRAINZMIRROR="https://musicbrainz.org"` | OPTIONAL :: Only change if using a different mirror |
| `-e MBRATELIMIT=1` | OPTIONAL: musicbrainz rate limit, musicbrainz allows only 1 connection per second, max setting is 10 :: Set to 101 to disable limit |
| `-e ARL_TOKEN="08d108d108d108d108d108d108d108d1"` | User token for dl client, for instructions to obtain token: https://notabug.org/RemixDevs/DeezloaderRemix/wiki/Login+via+userToken |
| `-e LIST=both` | both or missing or cutoff :: both = missing + cutoff :: missng = lidarr missing list :: cutoff = lidarr cutoff list |
| `-e SkipFuzzy=true` | true = enabled :: This will skip fuzzy searching for artists that have linked artist id for dl client (Various Artist is always fuzzy searched) |
| `-e Concurrency=3` | Number of concurrent processes (downloads and caching threads) |
| `-e quality=FLAC` | FLAC or 320 or 128 :: 320/128 are MP3 downloads, FLAC is lossless... |
| `-e MatchDistance="10"` | Set as an integer, the higher the number, the more lienet it is. Example: A match score of 0 is a perfect match :: For more information, this score is produced using this function: [Algorithm Implementation/Strings/Levenshtein distance](https://en.wikibooks.org/wiki/Algorithm_Implementation/Strings/Levenshtein_distance) |
| `-e FolderPermissions=766` | Based on chmod linux permissions |
| `-e FilePermissions=666` | Based on chmod linux permissions |

# Script Information
* Script will automatically run when enabled, if disabled, you will need to manually execute with the following command:
  * From Host CLI: `docker exec -it amd /bin/bash -c 'bash /config/scripts/download.bash'`
  * From Docker CLI: `bash /config/scripts/download.bash`
  
## Directories:
* <strong>/config/scripts</strong>
  * Contains the scripts that are run
* <strong>/config/logs</strong>
  * Contains the log output from the script
* <strong>/config/cache</strong>
  * Contains the artist data cache to speed up processes

<br />

# Lidarr Configuration Recommendations

## Media Management Settings:
* Disable Track Naming
  * Disabling track renaming enables synced lyrics that are imported as extras to be utilized by media players that support using them

#### Track Naming:

* Artist Folder: `{Artist Name}{ (Artist Disambiguation)}`
* Album Folder: `{Artist Name}{ - ALBUM TYPE}{ - Release Year} - {Album Title}{ ( Album Disambiguation)}`

#### Importing:
* Enable Import Extra Files
  * `lrc,jpg,png`

#### File Management
* Change File Date: Album Release Date
 
#### Permissions
* Enable Set Permissions
<br />
<br />
<br />
<br /> 


# Credits
- [Original Idea based on lidarr-download-automation by Migz93](https://github.com/Migz93/lidarr-download-automation)
- [Deemix download client](https://deemix.app/)
- [Musicbrainz](https://musicbrainz.org/)
- [Lidarr](https://lidarr.audio/)
- [Algorithm Implementation/Strings/Levenshtein distance](https://en.wikibooks.org/wiki/Algorithm_Implementation/Strings/Levenshtein_distance)
- Icons made by <a href="http://www.freepik.com/" title="Freepik">Freepik</a> from <a href="https://www.flaticon.com/" title="Flaticon"> www.flaticon.com</a>

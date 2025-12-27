# Soularr - Automated Music Downloads from Soulseek

Soularr is a Python-based automation tool that bridges **Lidarr** (music library manager) with **Soulseek** (peer-to-peer file sharing network) via **slskd** (modern Soulseek client).

## How It Works

1. **Reads** your wanted albums/artists from Lidarr's queue
2. **Searches** for those albums on the Soulseek network using slskd
3. **Downloads** matching files through slskd
4. **Triggers** Lidarr to import the completed downloads automatically

This creates a fully automated, hands-off music acquisition pipeline!

## Prerequisites

Before using Soularr, you need:

1. **Lidarr** or **Lidarr on Steroids (lidarr-deemix)** installed and configured with artists/albums
2. **slskd** installed with a valid Soulseek account

## Setup Instructions

### 1. Get Your Lidarr API Key
- Open Lidarr → Settings → General → API Key
- Copy this key for the Soularr configuration

### 2. Configure slskd API Key
- Open slskd → Options → API Keys
- Create a new API key with administrator role
- Copy this key for the Soularr configuration

### 3. Configure Soularr
When installing Soularr, provide:
- **Lidarr API Key**: From step 1
- **Lidarr Host URL**: Use `http://lidarr:8686` for standard Lidarr or `http://lidarr-deemix:8686` for Lidarr on Steroids
- **slskd API Key**: From step 2
- **slskd Host URL**: Default is `http://slskd:5030`

## Features

- **Automatic Searching**: Finds music on Soulseek based on your Lidarr wanted list
- **Quality Preferences**: Configurable file type preferences (FLAC, MP3 320, etc.)
- **Smart Matching**: Intelligent album and track matching with configurable thresholds
- **Multi-disc Support**: Handles multi-disc releases
- **Region Filtering**: Filter releases by country/region
- **Stalled Download Handling**: Automatically handles stuck downloads
- **Track Search Fallback**: Searches for individual tracks if album not found

## Folder Info

| Root Folder | Container Folder | Description |
|-------------|------------------|-------------|
| /runtipi/app-data/soularr/data | /data | Configuration files |
| /runtipi/media/downloads/complete | /downloads | Shared download directory with slskd |

## Important Notes

- Soularr runs as a background service with no web UI
- Check the container logs to monitor activity: `docker logs soularr`
- The script runs at the configured interval (default: every 5 minutes)
- Ensure all three services (Lidarr/Lidarr-deemix, slskd, Soularr) are on the same Docker network

## Troubleshooting

### Connection Issues
- Verify API keys are correct
- Ensure Lidarr and slskd are running and accessible
- Check that all services are on the `tipi_main_network`

### Downloads Not Importing
- Verify the download paths match between services
- Check Lidarr's download client settings
- Review Soularr logs for errors

## Links

- [GitHub Repository](https://github.com/mrusse/soularr)
- [Official Website](https://soularr.net)
- [Configuration Documentation](https://github.com/mrusse/soularr#configuration)

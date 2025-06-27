# Rhombus Camera Footage Copy Script

## Overview

This script allows you to copy recorded footage from Rhombus cameras to a pre-defined location for onsite or offsite storage. It provides flexible options for copying footage from specific cameras or entire locations within specified time windows.

## Prerequisites

Before using this script, you'll need to set up API credentials in the Rhombus console:

1. **API Key** (Required): Create an API key in the Rhombus console under "API Management"
2. **Certificate** (Optional): Create a certificate in the Rhombus console under "API Management" 
3. **Private Key** (Optional): Create a private API key in the Rhombus console under "API Management"

## Command Line Arguments

### Required Parameters

| Parameter | Short | Description | Required |
|-----------|-------|-------------|----------|
| `--api_key` | `-a` | Rhombus API key for authentication | ✅ Yes |

### Optional Parameters

| Parameter | Short | Description | Required |
|-----------|-------|-------------|----------|
| `--cert` | `-c` | Rhombus certificate for enhanced security | ❌ No |
| `--private_key` | `-p` | Rhombus private API key for enhanced security | ❌ No |
| `--start_time` | `-s` | Start time in epoch seconds for recording period | ❌ No |
| `--duration` | `-u` | Duration in seconds for the video clip | ❌ No |
| `--debug` | `-g` | Enable debug mode for troubleshooting | ❌ No |
| `--usewan` | `-w` | Enable WAN mode for offsite operation | ❌ No |
| `--location_uuid` | `-loc` | UUID of the location to copy footage from | ❌ No |
| `--camera_uuid` | `-cam` | UUID of specific camera to copy footage from | ❌ No |

## Usage Examples

### Copy footage from a specific camera
```bash
python copy_footage_script_threading.py -a YOUR_API_KEY -cam CAMERA_UUID -s 1640995200 -u 3600
```

### Copy footage from an entire location
```bash
python copy_footage_script_threading.py -a YOUR_API_KEY -loc LOCATION_UUID -s 1640995200 -u 3600
```

### Copy footage with debug mode enabled
```bash
python copy_footage_script_threading.py -a YOUR_API_KEY -cam CAMERA_UUID -s 1640995200 -u 3600 -g
```

### Copy footage for offsite operation
```bash
python copy_footage_script_threading.py -a YOUR_API_KEY -cam CAMERA_UUID -s 1640995200 -u 3600 -w
```

## Finding UUIDs

### Camera UUID
To find a camera's UUID, use the Rhombus API endpoint:
```
GET https://api.rhombussystems.com/api/camera/getCameraConfig
```

### Location UUID  
To find a location's UUID, use the Rhombus API endpoint:
```
GET https://api.rhombussystems.com/api/location/getLocations
```

## Time Format

The script uses **epoch seconds** (Unix timestamp) for time parameters. You can convert between human-readable dates and epoch seconds using online converters like:
- [Epoch Converter](https://www.epochconverter.com/)
- [Unix Timestamp Converter](https://www.unixtimestamp.com/)

### Example Time Conversion
- **Human readable**: January 1, 2022 12:00:00 PM UTC
- **Epoch seconds**: 1640995200

## Features

- **Multi-threaded copying**: Efficient parallel processing for faster transfers
- **Flexible targeting**: Copy from specific cameras or entire locations
- **Time-based filtering**: Specify exact start times and durations
- **Debug mode**: Troubleshooting capabilities for development and testing
- **WAN support**: Operate remotely with offsite storage capabilities
- **Security options**: Optional certificate and private key authentication

## Error Handling

The script includes comprehensive error handling and logging to help identify and resolve issues during the copying process. Enable debug mode (`-g`) for detailed troubleshooting information.

## Security Considerations

- Store API credentials securely and never commit them to version control
- Use certificates and private keys for enhanced security in production environments
- Consider network security when copying footage over WAN connections
- Ensure proper access controls on destination storage locations

## Related Files

- `copy_footage_script_threading.py` - Main script file
- `logging.py` - Logging utilities
- `mpd-info.py` - Media presentation descriptor utilities 
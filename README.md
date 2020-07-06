# ZoomStatus
A windows utility to get the status of a Zoom Meeting (Mute, Video, Screen Share, etc.)

## Usage
The script getZoomStatus.py is called without any parameters.  The results will be returned as JSON format.  Special thanks to https://github.com/yinkaisheng/Python-UIAutomation-for-Windows for doing all of the heavy lifting.  It uses the UIAutomation and accesibility features in windows to detect the Zoom windows and meeting controls.  It then extracts the text from the button control (i.e. Mute vs. Unmute) to determine the status.  The intention of this is to be used by other utilities such as a StreamDeck plugin https://github.com/smitmartijn/streamdeck-zoom-plugin.

## Examples

Zoom Meeting in progress, but muted, not sharing video, and not sharing screen.
{"statusZoom": "open", "statusMute": "muted", "statusVideo": "stopped", "statusShare": "stopped"}

Zoom Meeting not in progress
{"statusZoom": "closed", "statusMute": "muted", "statusVideo": "stopped", "statusShare": "stopped"}

Zoom Meeting in progress, unmuted, video is being shared, but not screen sharing.
{"statusZoom": "open", "statusMute": "unmuted", "statusVideo": "stopped", "statusShare": "stopped"}

## Limitations
Currently this program works by searching for the window control with classnames of ZPContentViewWndClass and ZPControlPanelClass.  These are the names of the windows when you have a window open called "Zoom Meeting" and down at the bottom is has "Mute, Start Video, Security, Participants, Chat, Share Screen, Record, Reactions and End." If you have the "docked" Zoom control window which is common during screen sharing this script currently does not work. There could be other limitations based on my Zoom Settings.  Please let me know if you receive an error.

It currently takes about 2 seconds to query all of the windows and get the Zoom Status.  I am sure this can be optimized and I am open to any suggestions.  However, there might be a slight delay between a change in the status in Zoom and the results of this script.

This method can be used to determine if recording is currently in progress, stopped, or paused.  However, this increases the time to run the script and is commented out at this time.

## Requirements
I am currently using Python 3.8.  It may work on other versions, but I am not certain.  You also need to install uiautomation ("pip install uiautomation"). 



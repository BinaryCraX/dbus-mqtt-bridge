# dbus-mqtt-bridge
a bridge to link mqtt and dbus

# ToDo
- [X] receive DBus-Signal
- [X] send MQTT-Message
- [ ] MQTT-TLS-Support
- [ ] react on DBus-property-change
- [ ] function-descriptions

# Example-Config
Following example-config subscribes for the property changed signal on DBus and
publishes changes to the selected MQTT-Topic when the playback-state changes.
Put this code into a "config.json" file in the working-directory.
```
{
	"Dbus": { },
	"Mqtt": {
		"Servers": ["tcp://server:1883"],
		"ClientID": "MediaPC",
		"Username": "",
		"Password": ""
	},
	"Mapping": [
	{
		"Mqtt": {
			"Topic": "vlc"
		},
		"Dbus": {
			"Type": "Signal",
			"Path": "/org/mpris/MediaPlayer2",
			"Interface": "org.freedesktop.DBus.Properties",
			"Sender": "org.mpris.MediaPlayer2.vlc",
			"StructPath": "[1].['PlaybackStatus']",
			"RemoveQuotmark": true
		},
		"Mode": "passtrough"
	}
	]
}
```

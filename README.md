# PSMS-OSVR-Connector
Plugin for OSVR that uses PSMoveService to connect HMD, left, and right hands to PS Move controllers.

# How to use 
- Copy *inf_psmove_osvr_connector.dll* into your osvr-plugins-0 folder.
- Copy the *PSMoveClient_CAPI.dll* from your PSMoveService folder into the root OSVR server folder (next to osvr_server.exe)
- Add the following to your osvr_server_config.json file.
- To map controller buttons, see the inf_psmove_osvr_connector.json file from the project source for paths.

To specify which controller should be used for which tracker, include this in your osvr server config:
```
  "drivers": [{
		"plugin": "inf_psmove_osvr_connector",
		"driver": "PSMSDevice",
		"params": {
			"hmdController": 0,
			"leftHandController": 1,
			"rightHandController": 2
		}
	}],
	"aliases": {
		"/me/head": "/inf_psmove_osvr_connector/PSMSDevice/semantic/hmd",
		"/me/hands/left": "/inf_psmove_osvr_connector/PSMSDevice/semantic/left",
		"/me/hands/right": "/inf_psmove_osvr_connector/PSMSDevice/semantic/right"
	}
```

Where 0, 1, and 2 are the *controller ID* in PSMoveConfig of the controllers you wish to map.

If you want to use just the "/me/head" then remove the two other controller from both Params and Aliases.

TODO (priority in order):
- Offsets (You can do this with osvr natively I think)
- Auto-Reconnect to PSMS

**If you have any issues**
- Start PSMS before OSVR Server
- Tested with PSMS alpha ver. 8.2.0
- You need to install Visual Studio 2015 C++ Redistributable from [here](https://www.microsoft.com/en-au/download/details.aspx?id=48145), or just Google it.
- Using older PSMoveService dll's is not supported and may or may not cause problems.
- This works as a headtracker for OSVR-Steamvr, but OSVR-Steamvr doesn't seem to support OSVR defined controllers at the moment. So you can use a conjunction of this and PSMove Steamvr Bridge for full room scale support with PSMoveService. (Which is what I am currently using)

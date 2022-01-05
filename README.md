Stand alone container using https://github.com/AndBobsYourUncle/hassio-addons/tree/master/google-assistant-webserver as a starting point.

## Installation instructions:
1. Deploy docker image from `ghcr.io/sammy1am/google-assistant-webserver:master`.  Map ports `9324:9324` and `5000:5000`, map path `/full/path/to/appdata/folder:/data`.
2. Check that you can see `http://containerip:9324`, but don't use this page to authenticate.
3. Run the following commands: 
```
export LC_ALL=C.UTF-8
export LANG=C.UTF-8
google-oauthlib-tool --client-secrets /data/client.json --scope https://www.googleapis.com/auth/assistant-sdk-prototype --save --headless
```
and follow the prompt to save the credentials.

4. Copy credentials from their generated location to `/data/cred.json`
5. Restart the container.


Add-on integration
--------------------------
You can add the below to your config.yaml then call notify.google_assistant or notify.google_assistant_command to broadcast a message accross your google homes or send an arbitrary command.

Send Broadcast

```yaml
notify:
  - name: Google Assistant
    platform: rest
    resource: http://[your.hassio.IP]:5000/broadcast_message
```

Send Google Assistant Command

```yaml
notify:
  - name: Google Assistant Command
    platform: rest
    resource: http://[your.hassio.IP]:5000/command?message=google_command
```

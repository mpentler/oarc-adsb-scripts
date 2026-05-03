# OARC ADS-B feed client

- **PLEASE** only feed us if you are part of OARC. THat is the whole point. See https://www.oarc.uk for details!
- These scripts aid in setting up your current ADS-B receiver to feed the [OARC ADS-B map](https://adsb.oarc.uk/).
- They will not disrupt any existing feed clients already present.
- MLAT is supported - specify a username when asked to enable this.

## 1: Find antenna coordinates and elevation

Coordinates: <https://www.mapcoordinates.net/en>
Elevation: <https://www.freemaptools.com/elevation-finder.htm>

## 2: Install the feed client

```
curl -L -o /tmp/feed.sh https://raw.githubusercontent.com/mpentler/oarc-adsb-scripts/master/install.sh
sudo bash /tmp/feed.sh
```

## 3: Use netstat to check that your feed is working
The feed IP for the OARC ADS-B map is 44.31.91.230

```
netstat -t -n | grep -E '30004|31090'
```
Expected Output:
```
tcp        0    182 localhost:43530     44.31.91.230:31090      ESTABLISHED
tcp        0    410 localhost:47332     44.31.91.230:30004      ESTABLISHED
```

You can also check your ADS-B feed status (but not MLAT yet) at https://adsb.oarc.uk/myip/

### Update the feed client without reconfiguring

```
curl -L -o /tmp/update.sh https://raw.githubusercontent.com/mpentler/oarc-adsb-scripts/master/update.sh
sudo bash /tmp/update.sh
```

### If you encounter issues, please do a reboot and then supply these logs on Discord (last 20 lines for each is sufficient):

```
sudo journalctl -u oarc-adsb-feed --no-pager
```

### Display the configuration

```
cat /etc/default/oarc-adsb
```

### Changing the configuration

This is the same as the initial installation.
If the client is up to date it should not take as long as the original installation,
otherwise this will also update the client which will take a moment.

```
curl -L -o /tmp/feed.sh https://raw.githubusercontent.com/mpentler/oarc-adsb-scripts/master/install.sh
sudo bash /tmp/feed.sh
```

### Restart the feed client

```
sudo systemctl restart oarc-adsb-feed
```

### Show status

```
sudo systemctl status oarc-adsb-feed
```

### Removal / disabling the services

```
sudo bash /usr/local/share/oarc-adsb/uninstall.sh
```

If the above doesn't work, you can just disable the services and the scripts won't run anymore:

```
sudo systemctl disable --now oarc-adsb-feed
```

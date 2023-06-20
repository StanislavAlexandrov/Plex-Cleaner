# Fork Notice

This is a fork of the original Plex Cleaner project. It addresses an issue where the script would fail to find media files, resulting in "[NOT FOUND]" errors. It's a hacky solution, so use at your own risk! Always use the --test option first!

The problem lies in the mismatch between the file paths returned from Plex and the actual file paths on Synology devices. For example, Plex may return a path like /movies/..., whereas the actual media file resides at /volume1/media/movies.

To correct this issue, this fork allows you to manually specify the correct paths to your movie and TV series media files. You need to do this in the PlexCleaner.py file.

By default, the paths are empty strings. If they are not updated with the correct paths, the script will throw an error. Please make sure to provide both paths.

All other aspects of the Plex Cleaner project remain the same.

Refer to the original README for additional information about the usage and functionality of Plex Cleaner.

## Please update the script to version 1.94 to avoid problems with your server by creating too many devices

# Plex Cleaner

A Script to clean up space on your Plex Media Server!

Automatically delete watched episodes or movies. Lots of customizable options.

## Configuration

To begin make a copy of Cleaner.conf.default and rename it as Cleaner.conf. You can then make edits to the Cleaner.conf file with your own settings. Descriptions of the settings are in the PlexCleaner.py script.

Alternatively you can create a config file by running the script with the option --dump [Path to Config file].

    python PlexCleaner.py --dump "/path/to/config/file"

PlexCleaner will then create a config file at the path specified with example values. You can then make edits to the config file based on your preferences. The formatting is very specific for the config file, if you have difficulty editing it, you can edit the default values in the script and then run the `--dump` argument to create a properly formatted config file.

By default plex will check in the users home directory for a .plexcleaner file, then in the current directory for a .plexcleaner or Cleaner.conf file. If you stored the config file in another location you will need to load the config file using the `--config` argument.
To do so you would run PlexCleaner as:

    python PlexCleaner.py --config "/path/to/config/file"

If the script is updated and you need to update your config file without losing your settings you can run PlexCleaner with `--update_config` argument. This will add any new configuration settings without overwriting any of your settings in the config file.

After you have entered your settings, it is recommended you first run the script with the `--test` flag. The `--test` flag will run the script without performing any actions, and flagging files that would be marked for deletion, copying, or moving. Once you have determined that the output is correct, you can run the script without the `--test` flag. The `--test` flag will also output the token used to login so you don't have to leave login details in the script.

## Docker

You can find a dockerized version of this script here: <https://github.com/NitriKx/docker-Plex-Cleaner>

```
docker pull nitrikx/plex-cleaner
docker run -ti -v /path/to/config/folder nitrikx/plex-cleaner
```

## Crontab and monitoring with Healthchecks.io

Create an account on <https://healthchecks.io>, and create up a new health check.
Create a new file at `healthchecksio_id`, and paste your health check ID.

Set up a `crontab` entry to run the script every day at 4am:

```
$ crontab -e

0 4 * * * /opt/Plex-Cleaner/run_plex_cleaner.sh
```

## Support

If you want to support me (does not equal development): <br>
<a href="https://www.paypal.me/ngovil21/1" target=blank><img src=http://imgur.com/WSVZSTW.png alt="Buy Me a Coffee" height=75 width=150 align='center'></a> &nbsp;&nbsp; or &nbsp;&nbsp; <a href="https://www.paypal.me/ngovil21/3" target=blank><img src=http://imgur.com/gnvlm6n.jpg alt="Buy Me a Beer" height=75 width=150 align='center'></a>

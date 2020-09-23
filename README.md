# droplist

A simple systemd service to fetch *Do not Route Or Peer* records from the Spamhaus DROP list, and maintain them in an iptables chain.

## Requirements

The following packages are required for this service:

* iptables
* socat
* wget

## Installation

Download or clone the repo. Extract the ZIP archive, if necessary. Prepare the installation directory

    sudo mkdir -p /opt/droplist

Copy the script files and set up permissions

    sudo cp droplist* /opt/droplist/
    cd /opt/droplist
    sudo chown root:root droplist*
    sudo chmod 644 droplist.service
    sudo chmod 755 droplist_cmd
    sudo chmod 700 droplistd

Link to the service file from systemd

    cd /etc/systemd/system
    sudo ln -s /opt/droplist/droplist.service

Reload systemd and configure service to start automatically on reboot

    sudo systemctl daemon-reload
    sudo systemctl enable droplist

## Usage

| Function           | Shell Commands                           |
|--------------------|------------------------------------------|
| Start service      | `sudo service droplist start`            |
| Stop service       | `sudo service droplist stop`             |
| Check log messages | `sudo service droplist status`           |
| Update IP list     | `sudo /opt/droplist/droplist_cmd update` |

The update command can be called from a cronjob.

## Notes

* Check and modify access permissions to fit your application
* No responsibility for you locking yourself out of the system
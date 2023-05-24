# docker-nextcloud

## How to use

Clone repository on your server and edit the necessory variables in the `docker-compose.yml`. Then run to following command to start the container.

```bash
docker compose up -d
```

## Start on boot

To start container on boot make sure you have enabled docker service to start automatically

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

Then create a new file

```bash
sudo nano /etc/systemd/system/nextcloud-container.service
```

Paste the following content in the file and save

```
[Unit]
Description=Nextcloud docker container

[Service]
Restart=always
ExecStart=/usr/bin/docker compose -f /path/to/folder/docker-compose.yml up
ExecStop=/usr/bin/docker compose -f /path/to/folder/docker-compose.yml down

[Install]
WantedBy=local.target
```

Then run the following

```bash
sudo systemctl start nextcloud-container.service
sudo systemctl enable nextcloud-container.service
```

To check the status run the following command

```bash
sudo systemctl status nextcloud-container.service
```

## Known issues

### 1. Change permission to 0770 error

If you get error to change permission to 0770 on creating an admin account attach shell to the nextcloud-app container and add the following to the end of the `config/config.php` file.

```
  'check_data_directory_permissions' => false,
```

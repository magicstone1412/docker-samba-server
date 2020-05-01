Repo này du?c clone t? https://github.com/vgist/dockerfiles

Cho phép luu tr? t? Camera IP theo giao th?c SMBv1

M?u: 

```
docker create \
  --name=smb \
  --hostname=SMB-IP-15 \
  -p 137:137/udp \
  -p 138:138/udp \
  -p 139:139/tcp \
  -p 445:445/tcp \
  -v /mnt/camera:/mnt \
  --restart=unless-stopped \
skywirex/smb:v200501-latest
```

#### Volume:

- /mnt

#### Port:

- 137/udp
- 138/udp
- 139/tcp
- 445/tcp

#### Custom usage:

    docker run \
        -d \
        --name samba-server \
        -p 137:137/udp \
        -p 138:138/udp \
        -p 139:139/tcp \
        -p 445:445/tcp \
        -v /your/path:/mnt \
        gists/samba-server

#### Compose example:

    samba-server:
      image: gists/samba-server
      container_name: samba-server
      ports:
        - "137:137/udp"
        - "138:138/udp"
        - "139:139/tcp"
        - "445:445/tcp"
      volumes:
        - /your/path:/mnt
      environment:
        - PASSWORD=yourpassword
      restart: always


## Intro

A Valheim server.

## Setting up a sudo user

1. Setup ssh for another user and add them to sudoers

    ```
    sudo adduser ola
    sudo adduser ola sudo
    ```

    generate and save password somewhere. Send to them privately

2. Ask for their public SSH key

3. Add the key to their authorized_keys

    ```
    sudo su ola
    cd
    mkdir -p .ssh
    touch .ssh/authorized_keys
    chmod 0600 .ssh/authorized_keys
    vi .ssh/authorized_keys
    ```

    Then copy the public key into that file and save and exit

## Instructions for updating

1. From your local machine, SSH into the valheim server (using ola as example)

    ```
    ssh ola@valheim.moocar.me
    ```

2. stop the valheim server

    ```
    sudo service valheim stop
    ```

3. run the update script

    ```
    sudo su -c '/home/steam/Valheim/update.sh' steam
    ```

4. start the valheim server

    ```
    sudo service valheim start
    ```

5. To see the status of the server, run

    ```
    sudo service valheim status
    ```

6. To see live logs, run

    ```
    sudo journalctl -u valheim -b -f
    ```

## Backups

World saves are located in `/home/steam/.config/unity3d/IronGate/Valheim/worlds_local/`.

To copy the latest save file to your local machine, perform the following steps.

1. SSH into the server using your personal account (see above)

2. Copy the latest save files into your home directory

    ```
    sudo cp /home/steam/.config/unity3d/IronGate/Valheim/worlds_local/Ladlandia.{fwl,db} ~/
    ```

3. From your **local machine**, run the following

    ```
    scp ola@valheim.moocar.me:~/Ladlandia.{fwl,db} ./
    ```

4. You should now see two new files in your local. `Ladlandia.db`, and `Ladlandia.fwl`.

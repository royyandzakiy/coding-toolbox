## compact HDD

- close docker desktop
- `wsl --shutdown`
- open admin terminal > diskpart
    ```bash
        select vdisk file="C:\Users\royya\AppData\Local\Docker\wsl\disk\docker_data.vhdx"
        attach vdisk readonly
        compact vdisk
        detach vdisk
        exit
    ```
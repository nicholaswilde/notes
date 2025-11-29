# systemctl

## Reset the Failed State

Sometimes the "failed" state can be sticky. If the unit still appears in a "failed" list, you can explicitly clear it. (The daemon-reload usually handles this, but this is a good command to know.)

=== "root"

    ```shell
    systemctl reset-failed homelab-pull.service
    ```

=== "sudo"

    ```shell
    sudo systemctl reset-failed homelab-pull.service
    ```

# Ansible Role: OnDemand exporter

This role installs the [OnDemand exporter](https://github.com/OSC/ondemand_exporter) for Prometheus on Linux hosts, and configures a systemd unit file so the service can run and be controlled by systemd.

## Requirements

You have a working Open OnDemand host.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    ondemand_exporter_version: '0.10.0'

The version of OnDemand exporter to install. Available releases can be found on the [releases](https://github.com/OSC/ondemand_exporter/releases) listing in the OnDemand exporter repository.

If you change the version, the `ondemand_exporter` binary will be replaced with the updated version, and the service will be restarted.

    ondemand_exporter_arch: 'amd64'
    ondemand_exporter_download_url: https://github.com/OSC/ondemand_exporter/releases/download/v{{ ondemand_exporter_version }}/ondemand_exporter-{{ ondemand_exporter_version }}.linux-{{ ondemand_exporter_arch }}.tar.gz

The architecture and download URL for ondemand exporter. If you're on a Raspberry Pi running Raspbian, you may need to override the `arch` value with `armv7`.

    ondemand_exporter_bin_path: /usr/local/bin/ondemand_exporter

The path where the `ondemand_exporter` binary will be installed.

    ondemand_exporter_host: 'localhost'
    ondemand_exporter_port: 9301

Host and port on which ondemand exporter will listen.

    ondemand_exporter_options: ''

Any additional options to pass to `ondemand_exporter` when it starts, e.g. `--collector.apache.status-url` if you want to change the location of Apache's mod_status URL.

    ondemand_exporter_state: started
    ondemand_exporter_enabled: true

Controls for the `ondemand_exporter` service.

## Dependencies

None.

## Example Playbook

    - hosts: all
      roles:
        - role: mrobbert.ondemand_exporter

## License

MIT / BSD

## Author Information

This role was created in 2024 by Mike Robbert based on the code in the ansible-role-node_exporter written by Jeff Geerling.

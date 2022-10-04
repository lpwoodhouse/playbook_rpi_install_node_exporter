# Ansible Playbook: rpi_install_node_exporter

### Part of my Raspberry Pi cluster project

Sets the 4 levels of cpu temperature at which an increase in fan speed occurs.<br>
This play is for raspbian distros only.

## Requirements

None

## Role Variables

Available variables are listed below, along with default values (see ```defaults/main.yml```)
```shell
fan_level0: 75000
fan_level1: 80000
fan_level2: 85000
fan_level3: 90000
reboot_var: true
```
## Dependencies

None

## Example Playbook
```yaml
    - hosts: all
      vars:
        fan_level0: 60000
        fan_level1: 65000
        fan_level2: 70000
        fan_level3: 75000
        reboot_var: false
      roles:
        - rpi_fan_levels
```

## License

MIT

## Author Information

This role was created in 2022 by [Lee Woodhouse](https://www.leewoodhouse.com/)

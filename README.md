# fix-bash-bug

Update bash.

- Simple for debian stable
- I discover that I forget to add `squeeze-lts` repository to my previous stable hosts
- Previous previous stable need to compile bash

## Requirements

- trigger `bash` source dowload and compilation for `lenny`

## Role Variables

```yaml
fix_bash_bug_proxy: # we need this to download bash sources
```

## Dependencies

None

## Example Playbook

```yaml
- hosts: all
  roles:
    - role: fix-bash-bug
```

## License

BSD

## Author Information

Thierry Delamare

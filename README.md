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

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

## License

BSD

## Author Information

Thierry Delamare

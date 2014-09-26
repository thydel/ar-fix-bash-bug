# fix-bash-bug

Update bash.

- Simple for debian stable
- I discover that I forget to add `squeeze-lts` repository to my previous stable hosts
- Previous previous stable need to compile bash (only tested with `lenny`)

## Requirements

- trigger `bash` source dowload and compilation for `lenny` (depends on `gcc` and `bison`)

## Role Variables

``` yaml
fix_bash_bug_proxy:                      # we need this to download bash sources, OK if empty
fix_bash_bug_proxy_cache_valid_time: 300 # cache_valid_time for apt module
fix_bash_bug_src: /usr/local/src         # where to dowload and compile bash-3.2 for lenny
```

## Tags and Extra Variables

``` ShellSession
ansible-playbook fix-bash-bug.yml -t update -e gather_facts=False # apt update
ansible-playbook fix-bash-bug.yml -t newer                        # post lenny
ansible-playbook fix-bash-bug.yml -t lenny                        # lenny only
ansible-playbook fix-bash-bug.yml -t check -e gather_facts=False  # shellshock snippet test only
```

## Dependencies

- `thydel.runp`
- `thydel.version-ansible`
- `thydel.patch`

## Example Playbook

``` yaml
- hosts: all
  gather_facts: |
    {{ gather_facts | default(True) }}
  vars:
    fix_bash_bug_proxy: http://proxy.domain.tld:3128
  roles:
    - role: thydel.runp
    - role: thydel.version-ansible
    - role: thydel.patch
    - role: thydel.fix-bash-bug
```

## Bugs

Depencies not yet uploaded

## License

BSD

## Author Information

Thierry Delamare

# fix-bash-bug

Update bash on lenny and later debian after shellshock

- Simple update for debian stable
- Add `squeeze-lts` repository for previous stable (should have already been there)
- Compile `bash` from source for previous previous stable (only tested with `lenny`)
- Up to patchlvel 54 for CVE-2014-7169
- Up to patchlvel 55

Compile bash 3.2 from source for Debian Lenny to patch CVE-2014-6271, CVE-2014-7169
inspired by https://gist.github.com/86de50d30134129e44ef

Applying a set of patches is not idempotent friendly.  The `patch`
module we use is able to tell if a patch is already applied, but as
every new patch changes the `patchlevel` file we can only benefit
this ability for the first yet unapplied patch. Yet, as we know via
`patchlevel` what is the last applied patch we can skip already
applied patches.

Thus when a new set of patches is released and after changing the
`last_patch_number` argument of `lenny` include task file in the
`main` task file for the role you can reuse previous compile dir.

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
ansible-playbook fix-bash-bug.yml -t lenny -e 'compile=True'      # force recompile
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
```

## Warning

I presently dont know how to get a Makefile like behaviour from
ansible (date changes based idempotency)

If the patchlevel of bash-3.2 is bump up you *must* force running make
again by using `compile` extra var.

## Bugs

Should be two different role
- trivial post lenny
- convoluted lenny

## License

BSD

## Author Information

Thierry Delamare

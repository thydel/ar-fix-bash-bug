# Changelog

## Version 1.1.1

* cometic changes
* more local strings via set_facts
* coherent naming for all tasks
* remove useless when clauses
* remove useless roles inclusion from test
* better dry vs wet run and lenny vs other setup

## Version 1.1.0

* lenny patch for CVE-2014-7169 up to patchlevel 54
* add a test for CVE-2014-7169
* add a CHANGELOG

## Version 1.0.0

* debian wheezy via simple upgrade
* ubuntu via simple upgrade (no release check)
* debian squeeze by ensuring squeeze-lts repos is used
* debian lenny via recompilation after patch for CVE-2014-6271 up to
  patchlevel 52

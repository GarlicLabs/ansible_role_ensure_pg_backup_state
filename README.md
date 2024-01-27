# ensure_pg_backup_state

[![Validate infrastructure as code](https://github.com/garliclabs/ensure_pg_backup_state/actions/workflows/validation.yml/badge.svg)](https://github.com/garliclabs/ensure_pg_backup_state/actions/workflows/validation.yml)

TODO description

## Requirements

TODO

## Role Variables

TODO

## Development

TODO

### Testing

* Create venv: `python3 -m venv ./venv`
* Install pip requirements: `venv/bin/pip install -r pip_requirements.txt`
* Execute tests `venv/bin/molecule test`

### Linting & static security analyser

Both the linter and the static security analyser are running on each push on the github actions pipeline.  

* As linter [ansible-lint](https://ansible.readthedocs.io/projects/lint/) is used. For installation documentation see [ansible lint installing](https://ansible.readthedocs.io/projects/lint/)
  * Just run `ansible-lint`

* To check if there are any passwords, tokens... hardcoded, [kics](https://kics.io/index.html) is used to ensure a secure IaC repository.  
  * Run it locally `docker run -t -v $PWD:/path checkmarx/kics:latest scan -p /path -o "/path/"`

## Dependencies

None.

## License

GNU General Public License version 3

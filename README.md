# ensure_pg_backup_state

[![Validate infrastructure as code](https://github.com/garliclabs/ansible_role_ensure_pg_backup_state/actions/workflows/validation.yml/badge.svg)](https://github.com/garliclabs/ansible_role_ensure_pg_backup_state/actions/workflows/validation.yml)

This Role installs a Kubernetes-CronJob that Backups a Postgres Database-dump to a remote storage using https://github.com/GarlicLabs/backup_pg_to_remote_storage


## Requirements

A working Kubernetes Cluster

## Role Variables

* pg_backup_state: If the CronJob to backup the Databases should be installed or removed. Accepts `present` and `absent`
* pg_backup_namespace: The Namespace where the Secret and CronJob should be installed into. Namespace must exist beforehand.
* pg_backup_schedule: The schedule of the Cronjob. Default is everyday at midnight (`"0 0 * * *"`).
* pg_backup_config: The Content of the configuration Secret. An Example is found below. Please refer to [the Documentation](https://github.com/GarlicLabs/backup_pg_to_remote_storage) for more info.

Example:
```yaml
pg_backup_state: present
pg_backup_namespace: default
pg_backup_schedule: "0 0 * * *"
pg_backup_config:
  storage:
    s3:
      endpoint:  "s3.example.com"
      accessKey: "example"
      secretKey: "example"
      bucket:    "test"
    databases:
      - host:     "database.example.com"
        port:     5432
        username: "postgres"
        database: "postgres"
        password: "postgres"
        retention: 30

```


## Development

To use this role in your playbook, you can put it into your galaxy requirements file:

```yaml 
- name: ensure_pg_backup_state
  src: https://github.com/GarlicLabs/ansible_role_ensure_pg_backup_state
```

Then you can use it in your playbook:

```yaml
- name: Ensure state of pg backup
  hosts: all
  roles:
    - ensure_pg_backup_state
```

### Linting & static security analyser

Both the linter and the static security analyser are running on each push on the github actions pipeline.  

* As linter [ansible-lint](https://ansible.readthedocs.io/projects/lint/) is used. For installation documentation see [ansible lint installing](https://ansible.readthedocs.io/projects/lint/)
  * Just run `ansible-lint`

* To check if there are any passwords, tokens... hardcoded, [kics](https://kics.io/index.html) is used to ensure a secure IaC repository.  
  * Run it locally `docker run -t -v $PWD:/path checkmarx/kics:latest scan -p /path -o "/path/"`

## Dependencies

Ansible-core.
kubernetes.core.k8s collection.

## License

GNU General Public License version 3

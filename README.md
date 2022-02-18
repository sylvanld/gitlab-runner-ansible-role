# Gitlab Runner

Role to install gitlab runner service and register runners.

## Role Variables

| Name                  | Description                                                                                             | Default                                            |
| --------------------- | ------------------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| gitlab_url            | URL of the gitlab instance where runners will be registered                                             | https://gitlab.com/                                |
| gitlab_runners        | List of runner objects describing runners to be registered. Preferably defined per host in `hosts.yml`. | If not defined for a host, no runner is registered |
| gitlab_runner_version | Version of gitlab-runner package to be installed                                                        | latest                                             |

## Example Playbook

`inventory/hosts.yml`

```yaml
---
vms:
  hosts:
    192.168.1.29:
      gitlab_runners:
        - name: my_project_testing_runner
          executor: shell
          token: <token>
          tags: testing,my-project,foo

        - name: my_project_staging_runner
          executor: shell
          token: <token>
          tags: staging,my-project,foo
```

`playbook.yml`

```
- hosts: vms
  roles:
    - role: gitlab-runner
      gitlab_url: "https://gitlab.corp.example/"
```

## Author Information

Sylvan LE DEUNFF sledeunf@gmail.com

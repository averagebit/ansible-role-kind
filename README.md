# kind (Ansible Role)

[![CI](https://github.com/averagebit/ansible-role-kind/workflows/CI/badge.svg?event=push)](https://github.com/averagebit/ansible-role-kind/actions?query=workflow%3ACI)

## Description

Installs [Kind](https://kind.sigs.k8s.io/).

## Requirements

The role was developed and tested with the following Ansible versions.

| Name                                                   | Version     |
| ------------------------------------------------------ | ----------- |
| [ansible](https://pypi.org/project/ansible-base/)      | `>= 2.9.13` |
| [ansible-base](https://pypi.org/project/ansible-base/) | `>= 2.10.1` |
| [ansible-core](https://pypi.org/project/ansible-core/) | `>= 2.11.2` |

## Platforms

The role was tested on the following distributions and releases.

| Name   | Version |
| ------ | ------- |
| Ubuntu | `jammy` |

## Installation

`ansible-galaxy install averagebit.kind` will install the latest
stable release.

`ansible-galaxy install -r requirements.yml` will install the role
from a requirements file.

```yaml
# requirements.yml
---
roles:
  - name: averagebit.kind
    version: 1.0.0
```

## Variables

- `kind_os`
  - Default: `"linux"`
  - Description: The OS target for the binary.
- `kind_version`
  - Default: `"latest"`
  - Description: The version of the binary can be a specific version such as: `"0.14.0"`.
- `kind_owner`
  - Default: `"root"`
  - Description: The owner of the installed binary.
- `kind_group`
  - Default: `"root"`
  - Description: The group of the installed binary.
- `kind_mode`
  - Default: `"0755"`
  - Description: The permissions of the installed binary.
- `kind_bin_dir_mode`
  - Default: `"0755"`
  - Description: The permissions of the binary directory.
- `kind_bin_dir`
  - Default: `"/usr/local/share/kind"`
  - Description: The directory to install the binary in.
- `kind_bin_path`
  - Default: `"{{ kind_bin_dir }}/kind"`
  - Description: The full path to the binary.
- `kind_link_path`
  - Default: `"/usr/local/bin/kind"`
  - Description: The symlink path created to the binary.
- `kind_repo_url`
  - Default: `"https://kind.sigs.k8s.io"`
  - Description: The URL to the repository.
- `kind_file_url`
  - Default: `"{{ kind_repo_url }}/dl/v{{ kind_version }}/kind-{{ kind_os }}-{{ kind_architecture }}"`
  - Description: The URL to the file.
- `kind_version_url`
  - Default: `"https://api.github.com/repos/kubernetes-sigs/kind/releases/latest"`
  - Description: The URL to fetch the latest version from.
- `kind_checksum_url`
  - Default: `"{{ kind_file_url }}.sha256sum"`
  - Description: The URL to the checksum of the file.
- `kind_architecture`
  - Default: `"{{ kind_architecture_map[ansible_architecture] }}"`
  - Description: The architecture target for the binary.
- `kind_architecture_map`
  - Default: `{"aarch": "arm64", "aarch64": "arm64", "amd64": "amd64", "arm64": "arm64", "armhf": "armhf", "armv7l": "armhf", "ppc64le": "ppc64le", "s390x": "s390x", "x86_64": "amd64"}`
  - Description: The architecture map used to set the correct name
    according to the repository binary naming.

## Usage

```yaml
# playbook.yml
- hosts: servers
  roles:
    - role: averagebit.kind
      become: true # required unless specified at the playbooks top level
      tags: kind # (optional) convenience tag
  vars:
    - kind_version: latest # or a specific version such as: 0.14.0
```

## Legal

Copyright 2022 averagebit <[averagebit@pm.me](mailto:averagebit@pm.me)>

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

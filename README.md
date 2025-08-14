# Hetzner Cloud setup using Ansible

<!--toc:start-->
- [Hetzner Cloud setup using Ansible](#hetzner-cloud-setup-using-ansible)
  - [Prerequisites](#prerequisites)
    - [Conda](#conda)
    - [Ansible](#ansible)
    - [Requirements](#requirements)
  - [Prepare Hetzner Cloud](#prepare-hetzner-cloud)
    - [SSH key](#ssh-key)
    - [API Token](#api-token)
<!--toc:end-->

## Prerequisites

In order to get started trying out Hetzner Cloud, Kubernetes, Helm and other
tools, you need to prepare your local development environment. Luckily,
ansible is a python software, so you can leverage conda to get a suitable
python environment without impacting your system too much.

### Conda

- Follow steps at [miniforge (github)][1]
- See [reference zsh dotfile][2] for adapting .zshrc

```shell
conda create -n ansible python=3.13
```

```shell
conda activate ansible
```

### Ansible

See [Ansible Getting Started][3] for official documentation.
Inside `ansible` conda env, run the following.

```shell
pip install ansible
```

As miniforge is a very minimal python environment, you might need to install
additional dependencies so that ansible can run successfully. These requirements
come from the [dynamic inventory plugin][4] of hcloud.

```shell
pip install requests python-dateutil
```

The required minimum ansible version is `2.18.0`.

### Requirements

To install ansible requirements, simply run the following.

```shell
ansible-galaxy install -r requirements.yml
```

## Prepare Hetzner Cloud

After all the preparations have been done, we can prepare the Hetzner Cloud itself.

### SSH key

- Go to the [Hetzner Cloud Project Overview][5]
- Open your project
- Go to `Security` -> `SSH keys` and `Add SSH key`
- Add your SSH key and save it as `default`
- Make your `default` SSH key your `Default` key

### API Token

- Get a read/write API token for your Hetzner Cloud, see [official documentation][6].
- Paste the token into `files/hcloud.token` and use ansible vault to encrypt it.

```shell
ansible-vault encrypt files/hcloud.token
```

Remember the password as you'll need it in a second.

[1]: https://github.com/conda-forge/miniforge
[2]: https://github.com/mor4thii/dotfiles/blob/main/zsh/.zshrc
[3]: https://docs.ansible.com/ansible/latest/getting_started/get_started_ansible.html
[4]: https://docs.ansible.com/ansible/latest/collections/hetzner/hcloud/hcloud_inventory.html#ansible-collections-hetzner-hcloud-hcloud-inventory
[5]: https://console.hetzner.cloud/projects/
[6]: https://docs.hetzner.com/cloud/api/getting-started/generating-api-token

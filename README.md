# Hetzner Cloud setup using Ansible

## Prerequisites

In order to get started trying out Hetzner Cloud, Kubernetes, Helm and other tools, you need to prepare your local development environment.
Luckily, ansible is a python software, so you can leverage conda to get a suitable python environment without impacting your system too much.

### Conda

- Follow steps at [miniforge (github)](https://github.com/conda-forge/miniforge)
- See [reference zsh dotfile](https://github.com/mor4thii/dotfiles/blob/main/zsh/.zshrc) for adapting .zshrc 

```shell
conda create -n ansible python=3.13
```

```shell
conda activate ansible
```

### Ansible

See [Ansible Getting Started](https://docs.ansible.com/ansible/latest/getting_started/get_started_ansible.html) for official documentation.
Inside `ansible` conda env, run the following.

```shell
pip install ansible
```

As miniforge is a very minimal python environment, you might need to install additional dependencies so that ansible can run successfully.
These requirements come from the [dynamic inventory plugin](https://docs.ansible.com/ansible/latest/collections/hetzner/hcloud/hcloud_inventory.html#ansible-collections-hetzner-hcloud-hcloud-inventory) of hcloud.

```shell
pip install requests python-dateutil
```

The required minimum ansible version is `2.18.0`.

### Requirements

To install ansible requirements, simply run the following.

```shell
ansible-galaxy install -r requirements.yml
```

### API Token

Get a read/write API token for your Hetzner Cloud, see [official documentation](https://docs.hetzner.com/cloud/api/getting-started/generating-api-token).
Paste the token into `files/hcloud.token` and use ansible vault to encrypt it.

```shell
ansible-vault encrypt files/hcloud.token
```

Remember the password as you'll need it in a second.

# Hetzner Cloud setup using Ansible

## Prerequisites

In order to get started trying out Hetzner Cloud, Kubernetes, Helm and other tools, you need to prepare your local development environment.
Luckily, ansible is a python software, so you can leverage conda to get a suitable python environment without impacting your system too much.

### Conda

- Follow steps at https://github.com/conda-forge/miniforge
- See [reference zsh dotfile](https://github.com/mor4thii/dotfiles/blob/main/zsh/.zshrc) for adapting .zshrc 
- `conda create -n ansible python=3.13`
- `conda activate ansible`

### Ansible

- See https://docs.ansible.com/ansible/latest/getting_started/get_started_ansible.html
- Inside `ansible` conda env: `pip install ansible`

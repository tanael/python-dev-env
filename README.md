# python-dev-env

Fully prepared for use dev-env repo creating a VM dedicated to python
development, using `libvirt`, `packer` and `vagrant`.

## Preliminary info

Good to know:

 - username `pliskin`
 - password `ch4ngeMe`

The first time you try to log in as `pliskin` AND `root`, you will need to
change the default password.

## Provisioning with `packer`

Debian `buster` VMs using `packer`.

### Requirements

#### Preseed file

Examples of customised information:
  - country code
  - root password
  - username
  - user password
  - timezone
  - sudoer
  - packages

#### JSON variables

Some variables are provided through `variables.json`.

E.g:
```json
{
    "iso_version": "10.9.0",
    "iso_checksum": "47d35187b4903e803209959434fb8b65ead3ad2a8f007eef1c3d3284f356ab9955aa7e15e24cb7af6a3859aa66837f5fa2e7441f936496ea447904f7dddfdc20",
    "username": "pliskin",
    "password": "ch4ngeMe"
}
```

#### SSH authorized keys

Add a file named `authorized_keys_production` in `files`, containing the public
keys of `ssh` clients you want to be able to connect to your VM.

### Usage

Use makefile, e.g.:

```bash
make devenv
```

This will create all intermediary images with a `devenv.box` ready to be used
by `vagrant`.

## Deploying with `vagrant`

Vagrant based on `.box` image created with `packer`.

### Requirements

User specific variables are provided through `config.yaml`. Make sure such a file exists
and contains the necessary variables.

E.g:
```yaml
---
conf:
    vmuser: 'frodo'
    localuser: 'gimli'
    priv_key: 'id_rsa'
```

### Usage

Add the box, that we shall name `pythonbox`:

```bash
vagrant box add --name pythonbox /path/to/devenv.box
```

Then spin up the environment by running the following command from a folder
containing a `Vagrantfile`

```bash
vagrant up
```

# Comprehensive System Configuration and Software Deployment Playbook

This Ansible playbook automates the installation and configuration of various software components, including the configuration of Quectel modules, Skylark software, UHD (USRP Hardware Driver), and Docker along with an SDR Docker image. 

## Prerequisites

- Ansible installed on the control machine.
- Access to the target hosts with proper SSH credentials and sudo privileges.
- Necessary packages and dependencies for the software components.

## Playbook Overview

The playbook is divided into several sections:
1. **System Configuration**: Upgrades the OS, ensures all packages are up to date, installs necessary packages like `minicom`.
2. **Quectel Module Configuration**: Finds, verifies, and copies Quectel folders, installs USB drivers, configures Minicom, and updates firmware.
3. **Skylark Software Installation**: Copies Skylark software to the remote location and installs required packages.
4. **SDR Software Installation**: Installs UHD and its dependencies, builds UHD, and verifies the installation.
5. **SDR Docker Installation**: Installs Docker, verifies the installation, and pulls the SDR Docker image.

## Playbook Structure

### Variables

- `quectel_folder`: Path to the local Quectel files.
- `quectel_config_folder`: Path to the Quectel configuration scripts.
- `remote_quectel_folder`: Path on the remote host to store Quectel files.
- `skylark_folder`: Path to the local Skylark files.
- `skylark_cpe_folder`: Specific Skylark CPE folder.
- `remote_skylark_folder`: Path on the remote host to store Skylark files.
- `driver_versions`, `closest_versions`, `firmware_versions`, `skylark_basic_deb_files`, `skylark_deb_files`: Lists to store version information and package paths.

### Tasks

#### System Configuration
- Pinging hosts to ensure connectivity.
- Upgrading the OS and updating package cache.
- Installing `minicom`.

#### Quectel Module Configuration
- Finding and verifying Quectel folders.
- Copying folders to the remote location.
- Retrieving kernel version and determining the USB driver.
- Installing USB drivers and ensuring they are correctly installed.
- Configuring Minicom and updating firmware.

#### Skylark Software Installation
- Copying Skylark software to the remote location.
- Finding and installing basic and specific Skylark packages.

#### SDR Software Installation
- Updating apt cache and installing required packages.
- Cloning the UHD repository, building UHD, and verifying the installation.
- Running tests and downloading UHD images.

#### SDR Docker Installation
- Installing Docker and its dependencies.
- Adding Docker’s GPG key and repository.
- Verifying Docker installation and pulling the SDR Docker image.

### Additional Tests

The playbook includes additional tests to verify the success of critical steps, such as:

- Checking if UHD repository was cloned successfully.
- Ensuring UHD build directory exists and build was successful.
- Verifying Docker GPG key and repository were added successfully.
- Ensuring Docker and SDR Docker image installation was successful.

## Running the Playbook

To run the playbook, use the following command:

```sh
ansible-playbook -i inventory_file playbook.yml
```

Replace `inventory_file` with the path to your Ansible inventory file.

## Troubleshooting

- Ensure that the control machine has SSH access to the target hosts.
- Verify that the paths specified in the variables exist and are correct.
- Check the Ansible logs for detailed error messages in case of failures.

## License

This project is licensed under the MIT License.

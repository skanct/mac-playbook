# MacOS Ansible Playbook

This playbook, inspired by [Jeff Geerling](https://www.jeffgeerling.com/)'s
[mac-dev-playbook](https://github.com/geerlingguy/mac-dev-playbook), automates
the installation and configuration of most software I use on my Mac. While
automating macOS setups can be challenging, this playbook minimizes manual
steps, documenting any necessary ones for clarity and ease of use.

## Installation

Follow these steps to get started:

1. **Install Apple's Command Line Tools**: Run `xcode-select --install` to
   launch the installer.
2. **Clone or Download This Repository**: Save it to your local machine.
3. **Prepare Your Environment**:
   1. Navigate to the repository's directory.
   2. Create a Python virtual environment: `python3 -m venv venv`
   3. Activate the virtual environment: `. venv/bin/activate`
4. **Install Ansible**:
   1. Upgrade Pip for the latest features and security improvements:
      `pip3 install --upgrade pip`
   2. Install Ansible to manage your setup: `pip3 install ansible`
5. **Run the Playbook**: Execute `ansible-playbook main.yml --ask-become-pass`
   and enter your macOS account password when prompted for the 'BECOME'
   password.

> **Troubleshooting**: If you encounter Homebrew errors, you may need to accept
> Xcode's license or address other issues. Use `brew doctor` to diagnose and fix
> these problems.

### Running Specific Tasks

To run specific parts of the setup, use the `--tags` option with
`ansible-playbook`. Available tags include:

- `dotfiles`
- `homebrew`
- `mas` (Mac App Store)
- `nvim` (Neovim)
- `vscode` (Visual Studio Code)
- `osx` (macOS settings)
- `timezone`

**Example**:

```zsh
ansible-playbook main.yml -K --tags "dotfiles,homebrew"
```

> **Note:** Unlike the original playbook by Jeff Geerling, I manage my
> `dotfiles` using stow and have introduced tasks for `nvim`, `vscode`, and
> `timezone` adjustments.

## Dotfiles Management

My `dotfiles` ([Github][1] [GEANT)][2]) are managed through this playbook,
including the `.osx` shell script for optimizing macOS settings. To skip
`dotfiles` management, set `configure_dotfiles: no` in your configuration.

[1]: https://github.com/skanct/dotfiles
[2]: https://gitlab.geant.org/christos.kanellopoulos/dotfiles

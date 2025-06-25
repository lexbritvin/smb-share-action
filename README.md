# Set up SMB Share

Creates an SMB user and share on Windows, macOS, Linux runners with enhanced security and logging. This action enables
file
sharing between the host runner and remote systems or containers.

> ⚠️ **Warning**: This action is intended for use only in public isolated GitHub runners. Use it with caution on
> self-hosted runners as it may affect system configuration and security.

## Features

- 📁 **Cross-Platform**: Works on both Windows, macOS, Linux GitHub runners
- 🔒 **Enhanced Security**: Implements SMB 3.0+ encryption and secure defaults
- 🔑 **User Management**: Creates dedicated SMB user with proper permissions
- 🔄 **Automatic Configuration**: Handles all setup details automatically
- 📊 **Detailed Logging**: Provides comprehensive setup and verification information
- 🔗 **SSH Tunneling**: Access shares remotely through
  [SSH Command & Port Forwarding Action](https://github.com/marketplace/actions/ssh-command-port-forwarding)
  or [Set up SSH Server Action](https://github.com/marketplace/actions/set-up-ssh-server)

## Usage

```yaml
- name: Set up SMB Share
  uses: lexbritvin/docker-sidecar-action/setup-smb-share@main
  with:
    path: ${{ github.workspace }}
    share-name: github_workspace
    share-user: smbuser
    share-pass: ${{ github.run_id }}_${{ github.run_number }}
```

## Inputs

| Input        | Description                           | Required | Default   |
|--------------|---------------------------------------|----------|-----------|
| `path`       | Local directory path to share via SMB | Yes      |           |
| `share-name` | Name of the SMB share                 | Yes      | `shared`  |
| `share-user` | Username for SMB access               | Yes      | `smbuser` |
| `share-pass` | Password for SMB user                 | Yes      |           |

## Outputs

None. The action sets up the SMB share on the local system.

## Example Workflow

```yaml
jobs:
  share-files:
    runs-on: windows-latest  # or macos-latest, or ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Set up SMB Share
        uses: lexbritvin/smb-share@v1
        with:
          path: ${{ github.workspace }}
          share-name: workspace_share
          share-user: github_user
          share-pass: ${{ secrets.SMB_PASSWORD }}
```

## Security Considerations

- Use strong, unique passwords for SMB authentication
- The action enables SMB encryption by default where supported

## Common Use Cases

1. **Cross-Platform Development**: Access files from different operating systems
2. **Remote Build Environments**: Share build artifacts between systems
3. **Testing File Access**: Verify application file sharing capabilities

## License

This project is licensed under the terms of the [LICENSE](./LICENSE) file included in this repository.

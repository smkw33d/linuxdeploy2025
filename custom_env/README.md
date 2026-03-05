# Custom Environment Scripts

This directory contains customized deployment scripts for the 2025 fork of Linux Deploy.

## Ubuntu Bootstrap Script

The Ubuntu deployment script (`include/bootstrap/ubuntu/deploy.sh`) has been enhanced with:

### Changes from Original

1. **Default Suite Updated**: Changed from `xenial` (16.04, EOL 2021) to `noble` (24.04 LTS, current point release 24.04.4)

2. **Enhanced apt_repository() Function**:
   - Proper quoting for APT configuration directives
   - Added `APT::Sandbox::Seccomp "false"` for modern Ubuntu versions
   - Automatic configuration of security and updates repositories
   - Improved comments for better maintainability

3. **Updated Help Text**:
   - All supported Ubuntu versions listed (questing through precise)
   - Support end dates included
   - Architecture compatibility warnings:
     - i386 not supported in noble (24.04) and later
     - armel only supported in precise (12.04)

### Integration

To apply these changes to the main application:

1. The submodule at `app/src/main/assets/env` points to the upstream `meefik/linuxdeploy-cli` repository
2. This custom version should be copied over the submodule files before building:
    ```bash
    mkdir -p app/src/main/assets/env/include/bootstrap/ubuntu/
    cp custom_env/include/bootstrap/ubuntu/* app/src/main/assets/env/include/bootstrap/ubuntu/
    mkdir -p app/src/main/assets/env/include/bootstrap/debian/debootstrap/scripts/
    cp custom_env/include/bootstrap/debian/debootstrap/scripts/* app/src/main/assets/env/include/bootstrap/debian/debootstrap/scripts/
    ```
    Or using rsync:
    ```bash
    rsync -av custom_env/include/bootstrap/ubuntu/ app/src/main/assets/env/include/bootstrap/ubuntu/
    rsync -av custom_env/include/bootstrap/debian/debootstrap/scripts/ app/src/main/assets/env/include/bootstrap/debian/debootstrap/scripts/
    ```

### Maintenance

When updating the linuxdeploy-cli submodule, remember to reapply these customizations or maintain a separate fork of the linuxdeploy-cli repository.

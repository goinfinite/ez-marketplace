# Infinite Ez Marketplace

This repository stores the installation and uninstallation manifests for all marketplace catalog items supported by [Infinite OS](https://github.com/goinfinite/os).

## Manifest/Schema Properties

| Property               | Type     | Is Required? | Description                                                                                                                                                                                                                                                                                                                                                               |
| ---------------------- | -------- | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `manifestVersion`      | string   | yes          | The version of the manifest. This version changes whenever the manifest is updated, indicating the presence of new placeholders or new commands.                                                                                                                                                                                                                          |
| `slugs`                | []string | yes          | Reference names for the catalog item, which can include full names, acronyms, or any identifier related to the catalog item.                                                                                                                                                                                                                                              |
| `name`                 | string   | yes          | The name of the catalog item that the manifest represents.                                                                                                                                                                                                                                                                                                                |
| `type`                 | string   | yes          | The type of the catalog item, which indicates its purpose.<br/><br/>`app`: application with their own functionality, such as WordPress.<br/>`framework`: structured software abstraction providing tools and guidelines for development, such as Laravel.<br/>`stack`: sets of solutions for building a specialized development and production environment, such as LAMP. |
| `description`          | string   | yes          | A description of the catalog item that explains what it is, what it does, and its purpose.                                                                                                                                                                                                                                                                                |
| `registryImageAddress` | string   | yes          | The address of the container image used for deployment.                                                                                                                                                                                                                                                                                                                   |
| `launchScript`         | []string | yes          | Commands to install the catalog item. This is one of the main parts of the manifest, as it contains all the steps required to install dependencies, the catalog item itself, and configure it. This can include editing necessary files, changing file permissions, or using Infinite OS CLI commands when needed.                                                        |
| `minimumCpuMillicores` | integer  | no           | The minimum recommended CPU (in millicores).                                                                                                                                                                                                                                                                                                                              |
| `minimumMemoryBytes`   | integer  | no           | The minimum recommended RAM (in bytes).                                                                                                                                                                                                                                                                                                                                   |
| `estimatedSizeBytes`   | integer  | no           | The estimated disk size after installation (in bytes).                                                                                                                                                                                                                                                                                                                    |
| `avatarUrl`            | string   | yes          | The URL for the catalog item's image, used for illustration purposes.                                                                                                                                                                                                                                                                                                     |

## System Data Fields

The system's data fields are predefined values used by Infinite Ez to replace placeholders in installation commands. They are similar to the data fields in the manifests themselves, but these are provided by Infinite Ez. These placeholders are denoted by `%` at the beginning and end, such as `%randomUsername%`.

The repository will automatically substitute these placeholders with the appropriate values during the installation process. For example:

```bash
os mktplace install -s wp -f "locale:en_US" -f "adminUsername:%randomUsername%" -f "adminPassword:%randomPassword%" -f "adminMailAddress:%randomMail%"
```

In this example, `%randomUsername%` will be replaced by a randomly generated username. Same for `%randomPassword%` and `%randomMail%`, which will be replaced by a randomly generated password and email address, respectively.

Below is a table of all available system data fields for creating manifests:

| Name             | Type   | Description                                            |
| ---------------- | ------ | ------------------------------------------------------ |
| `randomUsername` | string | Randomly generated username for the installation.      |
| `randomPassword` | string | Randomly generated password for the installation.      |
| `randomMail`     | string | Randomly generated email address for the installation. |

This substitution also occurs with the data fields added directly in the manifest. The `name` of the data field, when added to a command between `%` as a placeholder, will be replaced by the value of that data field during installation.

> [!IMPORTANT]
> System data field auto-generated values must be escaped within the manifest itself. Infinite Ez won't append any character to the auto-generated values.

## Avatars

The avatars are images that represent the catalog item in the Infinite Ez marketplace. They are used for illustration purposes and are displayed in the marketplace interface.
We recommend using [Pixlr Express](https://pixlr.com/express/) to create or edit images for the marketplace. The file should be named `avatar.jpg` and have a resolution of 720x720 pixels.

> [!TIP]
> If you're creating a catalog item which already exists in the Infinite OS marketplace, you can use the existing avatar image from the [Infinite OS Marketplace repository](https://github.com/goinfinite/os-marketplace).

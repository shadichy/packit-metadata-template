# Metadata template

Template for ExtOS including metadata file, used by packit and instanz

## System structure

This is the filesystem structure of ExtOS

```text
/
├── instances/
|   └── <instanz instances>/
|       ├── .conf           # instance config
|       ├── .instance       # instance metadata
|       ├── .pkg_fstab      # package table
|       ├── overlay/
|       |   └── <file system>
|       └── workdir/
├── packages/
|   └── <packit packages>/
|       ├── <file system>
|       ├── .files          # list of all files in file system
|       ├── .packit         # package metadata
|       ├── .source         # package additional information
|       ├── packit-scripts/
|       |   └── <pre/post install scripts>
|       └── packit-compatible/
|           └── <compatibility layer>
└── systems/
    └── <system images>/
        ├── <file system>
        ├── .files          # list of all files in file system
        ├── .rootfs         # system image metadata
        ├── .source         # system image additional information
        └── packit-compatible/
            └── <compatibility layer>
```

## Standard formats

Standard system image, package, instance metadata formats

### System Images

The following is an example of an ExtOS system image

```json
{
 "id": "sample-rootfs",             # System image id
 "label": "SAMPLE ROOTFS",          # Name of the system image
 "version": "0.0.1",                # System image version
 "arch": "x86_64",                  # System image architecture
 "instanz_ver": "^0.0.1",           # Minimum required instanz version
 "packit_ver": "^0.0.1"             # Minimum required packit version
}
```

And this is an example of Arch Linux compatibility layer of this system image

```json
{
 "defaultPackages": [               # Provided packages in equivalent of Arch Linux
  {
   "id": "base-sample",             # Package id
   "version": "0.0.1-1"             # Package version
  }
 ]
}
```

### Packit Packages

The following is an example of an ExtOS package

```json
{
 "id": "sample-package",            # Package id
 "description": "Sample package",   # Package description
 "version": "0.0.1",                # Package version
 "arch": "x86_64",                  # Package architecture
 "packit_ver": "^0.0.1"             # Minimum required packit version
}
```

And this is an example of Arch Linux compatibility layer of this package

```json
{
 "name": "sample-package",          # Package name in equivalent of Arch Linux
 "version": "0.0.1",                # Package version
 "dependencies": [                  # Package dependencies in equivalent of Arch Linux
  {
   "id": "sample-dependency",       # Dependency package name
   "version": "0.0.1"               # Dependency package version
  }
 ],
 "provides": [                      # Provided packages/libraries
  {
   "id": "sample-library",          # Provided packages/library name
   "version": "0.0.1"               # Provided packages/library version
  }
 ]
}
```

### Instanz Instances

The following is an example of an ExtOS instance

```json
{
 "id": "sample-íntance",            # Instance id
 "label": "SAMPLE INSTANCE",        # Instance name
 "description": "",                 # Instance description
 "instanz_ver": "^0.0.1",           # Minimum required instanz version
 "root_img": "sample-rootfs",       # System image used by the instance
 "root_ver": "^0.0.1",              # System image version
 "packages": [                      # Installed packages
  {
   "id": "sample-package",          # Package id
   "version": "^0.0.1",             # Package version
   "files": []                      # Installed files of the package
  }
 ]
}
```

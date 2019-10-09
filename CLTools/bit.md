# Bit

Git style decentralized version control for your components

 If you want to transfer a component from one project to another, Bit knows exactly which additional components should go with it. If a change occurs in a component, Bit can identify which components are impacted by it and notify consumers that a version update is available.

```bash
npm install bit-bin -g
```

## Concepts

A Bit workspace is a collection that resides inside a project. A workspace contains all of the component information and provides the functionality to author, export, import, and install components. 

A Bit workspace has 3 parts:

- **workspace config** contains information about the Bit project configuration such as the package manager for installing components, the default compilers and testers, and the components code location. The `package.json` file has a `bit` section with all of the workspace configuration. Alternatively, a `bit.json` file at the project's root directory can store the information in a separate file. This configuration is editable by the user to fit the exact configuration of the project.
- **components map** defines the files that comprise each component. The `.bitmap` file at the project's root stores this information. This file is created by Bit as a result of different user actions (e.g. adding new components). To retain information about the component map, the `.bitmap` file should be committed to the Version Control tool.
- **collection** the workspace's [collection](https://docs.bit.dev/docs/concepts#collection) contains the content of components. By default, the component store is an extension to the git repository under `.git/bit` directory, but can be stored elsewhere, such as under a `.bit` folder.
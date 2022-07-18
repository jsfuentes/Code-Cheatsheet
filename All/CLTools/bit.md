# Bit

Git style decentralized version control for your components

- manages component dependencies
- change in one project component, notifies the others there is a version update
- Use in other projects as npm package

```bash
npm install bit-bin -g
```

## Concepts

A Bit workspace has 3 parts:

- **workspace config** contains information about the Bit project configuration such as the package manager for installing components, the default compilers and testers, and the components code location. The `package.json` file has a `bit` section with all of the workspace configuration. Alternatively, a `bit.json` file at the project's root directory can store the information in a separate file. This configuration is editable by the user to fit the exact configuration of the project.
- **components map** defines the files that comprise each component. The `.bitmap` file at the project's root stores this information. This file is created by Bit as a result of different user actions (e.g. adding new components). To retain information about the component map, the `.bitmap` file should be committed to the Version Control tool.
- **collection** the workspace's [collection](https://docs.bit.dev/docs/concepts#collection) contains the content of components. By default, the component store is an extension to the git repository under `.git/bit` directory, but can be stored elsewhere, such as under a `.bit` folder.

## Usage

```bash
bit add src/components/*
```
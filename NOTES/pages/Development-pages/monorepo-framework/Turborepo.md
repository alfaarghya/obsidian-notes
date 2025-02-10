![[logo-turborepo.webp]]

---
Turborepo achieves faster build times through smart caching and parallelization. It uses content-addressable storage to cache build artifacts and constructs a dependency graph to determine which tasks can be run in parallel.
In December 2021, Vercel acquired Turborepo through an acqui-hire of Jared Palmer and his team. This acquisition brought additional resources and support to grow and evolve Turborepo.
Although Turborepo has gained popularity and praise for its capabilities, it is still a relatively new tool (the latest version as of the search results is 1.1.16). Some users have reported inconsistencies and the need for further polishing for production usage.

## Important Concepts
#### **1] Build System**
A build system is a tool that automates the process of transforming source code written by developers into executable code that can be run on a computer. In the context of JavaScript and TypeScript projects, a build system performs tasks such as:
- Transpilation: Converting TypeScript code to JavaScript code.
- Bundling: Combining multiple JavaScript files into a single file or a smaller set of files to optimize loading and execution.
- Minification: Reducing the size of JavaScript files by removing unnecessary characters and optimizing the code.
- Testing: Running automated tests to ensure the correctness and reliability of the code.
- Linting: Analyzing the code for potential errors, style inconsistencies, and adherence to coding standards.
- Deployment: Preparing the built code for deployment to a production environment.
Examples of popular build systems in the JavaScript ecosystem include Webpack, Rollup, Parcel, and Vite

#### **2] Build System Orchestrator**
A build system orchestrator, like Turborepo, sits on top of the actual build systems and coordinates the execution of tasks across multiple packages or projects within a monorepo. Instead of directly performing tasks like transpilation or bundling, a build system orchestrator focuses on:
- Task Definition: Allowing developers to define tasks in a configuration file (e.g., `turbo.json`) that specify the commands to run for each task.
- Task Orchestration: Determining the order in which tasks should be executed based on their dependencies and optimizing the execution process.
- Caching: Intelligently caching the results of previous builds to speed up subsequent builds and avoid redundant work.
- Parallel Execution: Leveraging available system resources to run tasks in parallel, improving overall build performance.
Here's an example of how you might define tasks in a `turbo.json` file:

```json
{
  "$schema": "<https://turborepo.org/schema.json>",
  "pipeline": {
    "build": {
      "dependsOn": ["^build"],
      "outputs": ["dist/**"]
    },
    "test": {
      "dependsOn": ["build"],
      "outputs": []
    },
    "lint": {
      "outputs": []
    }
  }
}
```

In this example, the `build` task depends on the `build` tasks of its dependencies (indicated by `^build`), the `test` task depends on the `build` task, and the `lint` task has no dependencies. Turborepo will optimize the execution of these tasks based on their dependencies and cache the outputs for faster subsequent builds.

#### **3] Monorepo Framework**
A monorepo framework provides a set of tools and conventions for managing projects that contain multiple packages or applications within a single repository. It focuses on:
- Dependency Management: Handling dependencies between packages within the monorepo, ensuring that packages can reference and use each other correctly.
- Workspace Configuration: Providing a way to define and configure workspaces, which are separate packages or projects within the monorepo.
- Shared Code: Facilitating the sharing of common code, utilities, and configurations across packages within the monorepo.
- Versioning: Managing the versioning of packages within the monorepo, often using a unified versioning scheme.
Examples of monorepo frameworks include Lerna, Nx, and Rush.

Here's an example of a monorepo structure using Lerna:
```
monorepo/
  ├── packages/
  │   ├── package-a/
  │   │   ├── src/
  │   │   ├── package.json
  │   │   └── tsconfig.json
  │   └── package-b/
  │       ├── src/
  │       ├── package.json
  │       └── tsconfig.json
  ├── package.json
  └── lerna.json
```

In this structure, the `packages` directory contains individual packages (`package-a` and `package-b`), each with its own `package.json` and source code. The root `package.json` and `lerna.json` files configure the monorepo and define the workspaces.

---
## Turborepo Features
Turborepo is a build system orchestrator designed to manage and optimize the execution of tasks across a monorepo. It sits on top of existing build systems and provides a layer of coordination and optimization.
Instead of directly performing build tasks like transpilation, bundling, or testing, Turborepo focuses on managing the execution of these tasks across the packages in your monorepo. It leverages intelligent caching, parallelization, and dependency graph awareness to speed up the overall build process.

1. **Caching**: Turborepo implements a caching mechanism to avoid unnecessary work and speed up subsequent builds. It caches the outputs of tasks based on their inputs (source files, dependencies, and configuration). If a task is executed again without any changes to its inputs, Turborepo can retrieve the cached output instead of re-executing the task.
	For example, consider a `build` task defined in your `turbo.json` file:

```json
{
  "$schema": "<https://turborepo.org/schema.json>",
  "pipeline": {
    "build": {
      "dependsOn": ["^build"],
      "outputs": ["dist/**"]
    }
  }
}
```

In this configuration, the `build` task depends on the `build` tasks of its dependencies (indicated by `^build`). Turborepo will cache the output of the `build` task in the `dist` directory. If the task is run again without any changes to its inputs, Turborepo will retrieve the cached output from the `dist` directory instead of re-executing the task.

2. **Parallelization**: Turborepo can identify independent tasks and run them in parallel, making efficient use of available system resources. By leveraging parallelization, Turborepo can significantly reduce the overall build time.

	For example, consider the following `turbo.json` configuration:

```json
{
  "$schema": "<https://turborepo.org/schema.json>",
  "pipeline": {
    "build": {
      "dependsOn": ["^build"],
      "outputs": ["dist/**"]
    },
    "test": {
      "dependsOn": ["build"],
      "outputs": []
    },
    "lint": {
      "outputs": []
    }
  }
}
```

In this example, the `test` task depends on the `build` task, but the `lint` task has no dependencies. Turborepo will recognize that the `lint` task can be run in parallel with the `build` task, optimizing the execution process.

3. **Dependency Graph Awareness**: Turborepo understands the dependency graph of your monorepo. It knows which packages depend on each other and ensures that tasks are run in the correct order based on those dependencies.
	For example, consider a monorepo with two packages: `package-a` and `package-b`. If `package-b` depends on `package-a`, Turborepo will ensure that the tasks for `package-a` are executed before the tasks for `package-b`.
	This dependency graph awareness allows Turborepo to build packages efficiently and avoid unnecessary rebuilds of downstream packages.

By leveraging caching, parallelization, and dependency graph awareness, Turborepo can significantly speed up the build process in a monorepo. It minimizes redundant work, optimizes resource utilization, and ensures that tasks are executed in the correct order based on package dependencies.

## **Turborepo Folder Structure**
Once the initialization process is complete or you have cloned the starter repository, you will notice a folder structure similar to the following:

```
my-turborepo/
  ├── apps/
  │   ├── docs/
  │   └── web/
  ├── packages/
  │   ├── ui/
  │   ├── eslint-config/
  │   └── typescript-config/
  ├── package.json
  ├── turbo.json
  └── pnpm-workspace.yaml
```
#### **End User Apps**
1. `apps/web`: This directory contains a Next.js website, which serves as the main user-facing application of your project.
2. `apps/docs`: This directory contains a documentation website built with Next.js. It is intended to host all the documentation related to your project.
#### **Helper Packages**
1. `packages/ui`: This directory contains UI packages that can be shared across different applications in your project. It may include reusable components, styles, or UI-related utilities.
2. `packages/typescript-config`: This directory contains a shareable TypeScript configuration. It allows you to maintain a consistent TypeScript configuration across all the packages and applications in your monorepo.
3. `packages/eslint-config`: This directory contains a shareable ESLint configuration. It helps enforce consistent coding standards and best practices across your project.

## Exploring Root `package.json`
The root `package.json` file is located at the top level of your Turborepo project and serves as the central configuration file for your monorepo. It contains scripts and dependencies that are shared across all the packages and applications within the monorepo.
![[root-packgeJson.webp]]
Let's break down each script:
1. **`build` Script**:
- When you run `npm run build` in the root of your Turborepo project, it executes the command `turbo run build`.
- This command tells Turborepo to run the `build` script defined in each package and application within the monorepo.
- Turborepo goes into all the `packages/*` and `apps/*` directories and runs `npm run build` inside them, provided they have a `build` script defined in their respective `package.json` files.
- The `build` script is typically used to compile, transpile, or bundle the code in each package and application.

2. **`dev` Script**:
- Running `npm run dev` in the root of your Turborepo project executes the command `turbo run dev --parallel`.
- This command tells Turborepo to run the `dev` script in each package and application within the monorepo, in parallel.
- Turborepo goes into all the `packages/*` and `apps/*` directories and runs `npm run dev` inside them, provided they have a `dev` script defined in their respective `package.json` files.
- The `dev` script is typically used to start the development server or watch for changes in each package and application.

3. **`lint` Script**:
- When you run `npm run lint` in the root of your Turborepo project, it executes the command `turbo run lint`.
- This command tells Turborepo to run the `lint` script defined in each package and application within the monorepo.
- Turborepo goes into all the `packages/*` and `apps/*` directories and runs `npm run lint` inside them, provided they have a `lint` script defined in their respective `package.json` files.
- The `lint` script is typically used to perform static code analysis and check for potential errors or style violations in each package and application.

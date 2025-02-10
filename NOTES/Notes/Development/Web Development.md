
# [[React.js]]

---

# [[TypeScript]]

---

# Monorepo
A monorepo, short for "monolithic repository," is a single repository that contains all the code for multiple projects or components of a larger application. Instead of having separate repositories for frontend, backend, and DevOps code, a monorepo consolidates everything into a single repository.
**Examples**
1. [https://github.com/code100x/daily-code](https://github.com/code100x/daily-code)
2. [https://github.com/calcom/cal.com](https://github.com/calcom/cal.com)

## Why Monorepos
1. **Shared Code Reuse**: One of the primary benefits of using a monorepo is the ability to easily share code between different services or projects. In a monorepo, you can have a dedicated directory for shared libraries, utilities, or components that can be used across multiple services.
2. 2. **Enhanced Collaboration**: Monorepos foster collaboration among team members by providing a centralized location for all the code. Developers can easily navigate and contribute to different parts of the project without the need to switch between multiple repositories.
3. **Optimized Builds and CI/CD**: Monorepos enable the use of specialized tools like TurboRepo, which offer smart caching and task execution strategies. These tools can significantly reduce build and testing times by leveraging the shared nature of the codebase.
4. 4. **Centralized Tooling and Configuration**: Managing build tools, linters, formatters, and other configurations becomes simpler in a monorepo. Instead of duplicating configurations across multiple repositories, you can have a single set of tools and configurations that apply to the entire project.

##  Monorepo Frameworks
1. **Lerna** ([https://lerna.js.org/](https://lerna.js.org/)): 
	Lerna is a popular tool for managing JavaScript monorepos. It provides features like package management, versioning, and publishing. With Lerna, you can easily manage dependencies, run scripts across multiple packages, and publish packages to npm.
	Example `lerna.json` configuration:
	```json
	{
	  "packages": ["packages/*"],
	  "version": "independent",
	  "npmClient": "yarn",
	  "useWorkspaces": true
	}
	```

2. **Nx** ([https://github.com/nrwl/nx](https://github.com/nrwl/nx)): 
	Nx is a powerful monorepo tool and build system developed by Nrwl. It offers a wide range of features, including code generation, dependency management, and advanced build optimization. Nx supports various frontend and backend frameworks, making it a versatile choice for monorepo development.
	Example `nx.json` configuration:
	```json
	{
  "npmScope": "myorg",
  "affected": {
    "defaultBase": "main"
	},
  "tasksRunnerOptions": {
    "default": {
      "runner": "@nrwl/workspace/tasks-runners/default",
      "options": {
        "cacheableOperations": ["build", "lint", "test", "e2e"]
      }
    }
  }
}
	```

1. **[[Turborepo]]** ([https://turbo.build/](https://turbo.build/)): 
	Turborepo is a high-performance build system for JavaScript and TypeScript codebases. While not strictly a monorepo framework, it provides powerful features for managing and optimizing monorepo builds. Turborepo focuses on fast incremental builds, caching, and efficient task execution.
	Example `turbo.json` configuration:
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
    }
  }
}
	```

2. **Yarn/npm Workspaces** ([https://classic.yarnpkg.com/lang/en/docs/workspaces/](https://classic.yarnpkg.com/lang/en/docs/workspaces/)): 
	Yarn and npm both provide built-in support for workspaces, which allow you to manage multiple packages within a single repository. Workspaces enable you to share dependencies across packages and link them together for development purposes.
	Example `package.json` configuration with Yarn workspaces:
	
	```json
{
  "private": true,
  "workspaces": ["packages/*"]
}
	```

---
# [[CI-CD]]

## Continuous Integration (CI)
Continuous Integration (CI) is a development practice where developers frequently integrate their code changes into a shared repository, preferably several times a day. Each integration is automatically verified by :
Building the project and 
Running automated tests. 
This process allows teams to detect problems early, improve software quality, and reduce the time it takes to validate and release new software updates.

## Continuous Deployment (CD)
As the name suggests, deploying your code `continuously` to various environments (dev/stage/prod)

![[architectureDiagram.webp]]
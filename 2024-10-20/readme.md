- [Micro Frontend](#micro-frontend)
  - [Module Federation](#module-federation) 

## Micro Frontend

- UI Architecture style about by sharing `FE UI code`.
- Platform-agnostic achievable by using https://single-spa.js.org/
- Independently Deployment of Runtime Dependency/package. [Module Federation](#module-federation) can achieve this by sharing code as runtime dependency.

### Module Federation

Code transport layer. Code will be shared as runtime dependency.

```shell
npx create-mf-app
```

- **Publish** : By using module federation, each component will be published as a package with file `remoteEntry.js`, this package can be hosted in bucket served through CDN.
- **Consume/Import** : Shared component will be fetched by host from remote using config file `remoteEntry.js`
- **Versioning package** :
  - Use https://unpkg.com/ with semantic versioning https://semver.org/. Eg : 
    - `^1.0.0` means version range `>= 1.0.0 but < 2.0.0` -> allow `patching` & `minor` version update, but not `major` version
    - `~1.0.0` means version range `>= 1.0.0 but < 1.1.0` -> only allow `patching` version update
- **How to safely import**:
  - In react use `Error Boundaries` https://legacy.reactjs.org/docs/error-boundaries.html . So when the component trigger an error , it will not take the whole site down. Only the component is not rendered
- **Typescript** :
  - Module federation doesn't support typescript, because Module Federation only shared runtime code, which is a vanilla js
  - How the host use typescript from shared code ? 
    - Create shared libary to manage the contract of typescript the @types manually or using code generator.
      ```shell
      src
        @types@remote
          MFPackage1
            index.d.ts
      ```
    - eg : in react host `tsconfig.json`
      ```json
      {
        "jsx": "react",
        "paths": ["src/@types/*"]
      }
      ```
    - Another solution : Create shared library to manage the contract of typescript
- **State management** :
  - Module federation doesn't share state
  - The host need to maintain the context
    ![shared-host-state](https://github.com/harryosmar/what-do-i-learn-today/blob/master/2024-10-20/arch1.png)
  - State manager choices : 
    - https://redux.js.org/, 
    - https://zustand-demo.pmnd.rs/ , 
    - https://jotai.org/








# webpack-cheat-sheet



<br><br>
<br><br>

# import

<br><br>

## Dynamic expressions in import()
- https://webpack.js.org/api/module-methods/#dynamic-expressions-in-import
- It is not possible to use a fully dynamic import statement, such as import(foo). Because foo could potentially be any path to any file in your system or project.
```
# Will not work
await import(path)

# Will work
await import('./anyHardcoded/path.js')
await import(/* webpackIgnore: true */ path);
```
  - The import() must contain at least some information about where the module is located. Bundling can be limited to a specific directory or set of files so that when you are using a dynamic expression - every module that could potentially be requested on an import() call is included. For example, import(`./locale/${language}.json`) will cause every .json file in the ./locale directory to be bundled into the new chunk. At run time, when the variable language has been computed, any file like english.json or german.json will be available for consumption.

<br><br>

### Magic Comments
```javascript
// Single target
import(
  /* webpackChunkName: "my-chunk-name" */
  /* webpackMode: "lazy" */
  /* webpackExports: ["default", "named"] */
  /* webpackFetchPriority: "high" */
  'module'
);

// Multiple possible targets
import(
  /* webpackInclude: /\.json$/ */
  /* webpackExclude: /\.noimport\.json$/ */
  /* webpackChunkName: "my-chunk-name" */
  /* webpackMode: "lazy" */
  /* webpackPrefetch: true */
  /* webpackPreload: true */
  `./locale/${language}`
);
```

<br><br>

#### webpackIgnore
```javascript
- import(/* webpackIgnore: true */ path);
```

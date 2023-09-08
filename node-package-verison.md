# Manage npm Dependencies Semantic Versioning
One of the biggest reasons to use a package manager, is their powerful dependency management. Instead of manually having to make sure that you get all dependencies whenever you set up a project on a new computer, npm automatically installs everything for you. But how can npm know exactly what your project needs? Meet the dependencies section of your package.json file.
```json
"package": "MAJOR.MINOR.PATCH"
"package_name" : "1.0.0"
```
## Use the Tilde-Character to Always Use the Latest Patch Version of a Dependency
o allow an npm dependency to update to the latest PATCH version, you can prefix the dependency’s version with the tilde (~) character. Here's an example of how to allow updates to any 1.3.x version.

```json
"package": "~1.3.x"
```

## Use the Caret-Character to Use the Latest Minor Version of a Dependency
Similar to how the tilde we learned about in the last challenge allows npm to install the latest PATCH for a dependency, the caret (^) allows npm to install future updates as well. The difference is that the caret will allow both MINOR updates and PATCHes.

```json
"package": "^1.x.x"
```

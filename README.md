# Get gradle version action 
(a fork of get npm version action: https://github.com/pchynoweth/action-get-npm-version)

This action extracts the version string from the build.gradle file.

## Inputs

### `file`

**Optional** The build.gradle file. Default `"build.gradle"`.

## Outputs

### `version`

the version inside build.gradle file.

## Example usage

```yaml

name: GET GRADLE VERSION

on:
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    outputs:
      version: ${{ steps.version.outputs.version }}                # <- put the version to output of the current job to share the version between different jobs
    steps:
      - uses: actions/checkout@v2
      
      
      
      - uses: thecodemonkey/action-get-gradle-version@master       # <- USE THIS ACTION TO READ THE VERSION FROM BUILD.GRADLE
        id: version                                                # <- give this step an id to access the output of the step
        
        
        
        
      - run: 'echo version ${{ steps.version.outputs.version }}'   # <- access the version
 
  deploy:
    runs-on: ubuntu-latest
    needs: build
    steps:
      - run: 'echo version ${{needs.build.outputs.version}}'       # <- access the version in another job
      
```

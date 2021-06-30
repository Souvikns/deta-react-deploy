# deta-react-deploy
Deploy react website on Deta


## Usage

```yaml
# This workflow will do a clean install of node dependencies, build the source code and run tests across different versions of node
# For more information see: https://help.github.com/actions/language-and-framework-guides/using-nodejs-with-github-actions

name: Deploy to Deta

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
  workflow_run:

jobs:
  build:

    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [12.x]

    steps:
    - uses: actions/checkout@v2
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v2
      with:
        node-version: ${{ matrix.node-version }}
    - run: npm ci
    - run: npm run build --if-present
    - uses: Souvikns/deta-react-deploy@v0.0.1
      with:
        deta-access-token: ${{ secrets.DETA_TOKEN }} #Deta access token https://docs.deta.sh/docs/cli/auth
        deta-name: 'Testing' #Deta Micro name https://docs.deta.sh/docs/cli/commands/#deta-clone
        deta-project: 'default' #Deta project name https://docs.deta.sh/docs/cli/commands/#deta-clone

```
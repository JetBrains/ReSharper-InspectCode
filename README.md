# JetBrains ReSharper InspectCode GitHub Action

C# static analysis on GitHub Actions using JetBrains ReSharper InspectCode.

[![official JetBrains project](https://jb.gg/badges/official-flat-square.svg)](https://confluence.jetbrains.com/display/ALL/JetBrains+on+GitHub)

## Usage

```yml
name: InspectCode

on:
  push:
    branches:
      - main
      - 'releases/*'
  pull_request:
    types: [opened, reopened]
  workflow_dispatch:
  
jobs:
  inspect-code:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
        with:
          submodules: recursive

      - name: Annotate
        uses: derigel23/ReSharper-InspectCode@516f3a14d72c8666911b8e2e1498441a93b2a222
        with:
          solution: ./YourSolution.sln
```

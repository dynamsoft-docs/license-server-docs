# This is a basic workflow to help you get started with Actions

name: CI

# Controls when the workflow will run
on:
  push:
    branches: 
    - main 

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains jobs called "Build-Main" and "Build-Preview"
  Build-Main:
    if: ${{ github.ref == 'refs/heads/main' }}
    uses: dynamsoft-docs/Docs-Template-Repo/.github/workflows/called-workflow-build-sync-production.yml@main
    with:
      doc-repo: license-server-docs
      doc-url: license-server/docs
    secrets: inherit
       

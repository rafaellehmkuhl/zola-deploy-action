# Zola Deploy Action

[![Build Status](https://img.shields.io/endpoint.svg?url=https%3A%2F%2Factions-badge.atrox.dev%2Fshalzz%2Fzola-deploy-action%2Fbadge&style=flat)](https://actions-badge.atrox.dev/shalzz/zola-deploy-action/goto)
![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/shalzz/zola-deploy-action?sort=semver)

A GitHub action to automatically build and deploy your [zola] site to the master
branch as GitHub Pages.

## Table of Contents

 - [Usage](#usage)
 - [Secrets](#secrets)
 - [Custom Domain](#custom-domain)

## Usage

```
on: push
name: Build and deploy on push
jobs:
  build:
    name: shalzz/zola-deploy-action
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
    - name: shalzz/zola-deploy-action
      uses: shalzz/zola-deploy-action@master
      env:
        PAGES_BRANCH: gh-pages
        BUILD_DIR: docs
        BUILD_FLAGS: --drafts
        TOKEN: ${{ secrets.TOKEN }}
```

## Secrets

 * `TOKEN`: [Personal Access key][] with the appropriate scope. If the
    repository is public the `public_repo` scope suffices, for private
    repositories the full `repo` scope is required. We need this to push
    the site files back to the repo.
    
    ( Actions already provides a `GITHUB_TOKEN` which is an installation token and does not trigger a GitHub Pages builds hence we need a personal access token )
    
    After creating your Personal Acess key you need to link it to a repository secret. For that, go to the Settings page of your repository and on the Secrets tab add a new secret with the same name used on your .yaml file and the same token value of your Personal Acess key.  
    

## Environment Variables
* `PAGES_BRANCH`: The git branch of your repo to which the built static files will be pushed. Default is `gh-pages` branch
* `BUILD_DIR`: The path from the root of the repo where we should run the `zola build` command. Default is `.` (current directory)
* `BUILD_FLAGS`: Custom build flags that you want to pass to zola while building. (Be careful supplying a different build output directory might break the action).

## Custom Domain

If you're using a custom domain for your GitHub Pages site put the CNAME 
in `static/CNAME` so that zola puts it in the root of the public folder
which is where GitHub expects it to be.

[zola]: https://github.com/getzola/zola
[Personal Access key]: https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line

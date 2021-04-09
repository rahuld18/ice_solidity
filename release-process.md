This document includes:
 - how to update remix.ethereum.org.
 - how to update remix-alpha.ethereum.org.
 - how to release remix IDE.

# remix-* release (npm release, github release) 
   
 - For a specifix module (lib/core/debug/ide/solidity/tests)
 - In a new branch, bump the version in package.json, push it and create PR.
 - Wait for tests completion.
 - merge PR
 - build the branch ( `npm run build` for remix-ide ).
 - execute `npm publish`.
 - create new `tag` ( e.g `git tag v0.6.1-alpha.2` ).
 - push the tag ( `git push --tag` ).
 - execute `gren changelog --generate -t <new tag>..<previous tag> --data-source=prs`.
 - in `changelog.md` remove the closed and non merged PR.
 - publish a release in github using the changelog.


# remix.ethereum.org update

This is not strictly speaking a release. Updating the remix site is done through the Travis build:

 - In remix-ide repository
 - Switch to the branch `remix_live`
 - Rebase the branch against master
 - Force push
 - https://travis-ci.org/ethereum/remix-ide
 - Click `More options`
 - Click `Trigger build`
 - Select `remix_live`
 - Click `Trigger custom build`
 - Once the build is finished (can take a while) and successful, check remix.ethereum.org is updated accordingly

# remix-alpha.ethereum.org update

This is not strictly speaking a release. Updating the remix-alpha site is done through the Travis build:

 - https://travis-ci.org/ethereum/remix-ide
 - Click `More options`
 - Click `Trigger build`
 - Select `Master`
 - Click `Trigger custom build`
 - Once the build is finished (can take a while) and successful, check remix-alpha.ethereum.org is updated accordingly
 
# beta testing remix

We publish a new release roughly every month and greatly appreciate support on beta testing. 

By giving report, beta testers help to:
 - verify viabilty (in term core and UX design) of new features
 - track possible regression
 - propose new update
 - contribute on reviewing / building Pull Request
 
# remix IDE release

 - git fetch origin master
 - git checkout origin/master
 - git checkout -b bumpVersion
 - update package.json version and version in terminal.js
 - create a PR and wait for test
 - merge PR
 - git fetch origin master
 - git checkout origin/master
 - git tag v(version-number)
 - git push --tags
 - github-changes -o ethereum -r remix-ide -a --only-pulls --use-commit-body --only-merges --between-tags previous_version...next_version
 - publish a release in github using the changelog
 - rm -rf node_modules
 - npm install
 - remove all soljson.js files in root folder
 - npm run build
 - npm publish

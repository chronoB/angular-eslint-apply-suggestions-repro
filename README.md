# AngularEslintBulkSuppressions

## Issue

This is a reproduction repo for using angular-eslint with the apply-suppressions options that was added to the eslint node.js api in version 10.1 [Docs](https://eslint.org/docs/latest/use/suppressions#usage-with-the-nodejs-api). 

This project was generated using [Angular CLI](https://github.com/angular/angular-cli) version 21.2.3 (commit https://github.com/chronoB/angular-eslint-apply-suggestions-repro/commit/5d907861adbdd89954a5fd2510e5d6a4a7ecf485).

I then added angular-eslint via `ng add angular-eslint` and updated eslint to version 10.1.0 (commit https://github.com/chronoB/angular-eslint-apply-suggestions-repro/commit/14966382169a70c6a368c45c2768bb51a3d98728).

Then I ran both ng lint and eslint to check if the both return 0 errors.

```sh
ng lint
npx eslint .
```

Afterwards I added a linting error (changed the selector of the app-component) and checked that both commands return the error (commit https://github.com/chronoB/angular-eslint-apply-suggestions-repro/commit/363f7a3a8a444ea7b21257609c8f90a083fdaedd).

Then I ran
```sh
npx eslint --suppress-all . # add eslint-suppressions.json
ng lint # still returns 1 error 
npx eslint . # does not return any error
```
(commit https://github.com/chronoB/angular-eslint-apply-suggestions-repro/commit/cd10de55a124930627187fc1ae230f1a77acd921)

## Proposed Fix
I created a patch in commit https://github.com/chronoB/angular-eslint-apply-suggestions-repro/commit/ffa2bd846a4fdf4290a89ac0e65246ec03c3e6df (located under patches/@angular-eslint+builder+21.3.1.patch) that adds the apply-suppressions option. I tested it both by running `ng lint --apply-suggestions` on its own and adding the apply-suggestions option in the angular.json and running `ng lint`. Both returned zero errors. I can't say anything about possible problems with backwards compatibility. 
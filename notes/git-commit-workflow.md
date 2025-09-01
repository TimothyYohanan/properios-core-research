# Git Commit Workflow
    $ VER=v<>.<>.<>
    $ ./scripts/pre-commit-fixup
    $ git add .
    $ git commit -m "$VER"
    $ git tag "$VER"
    $ git push origin master
    $ git push origin "$VER"

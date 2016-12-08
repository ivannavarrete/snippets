### Submodules

##### Add submodule

    git remote add <submodule_name> <submodule_repo.git>
    git subtree add --prefix <local_dir> <submodule_name> <submodule_branch>

##### Contribute changes back to submodule

    git subtree push --prefix <local_dir> <submodule_name> <new_submodule_branch>

Then open a pull request from `new_submodule_branch` into an existing branch in the submodule repo.

##### Get updates from submodule

    git fetch <submodule_name> [branch]
    git subtree pull --prefix <local_dir> <submodule_name> <submodule_branch> [--squash]

##### Tips

When pulling changes from subtrees, merge the commits with squash to avoid commit message repetition.

Whenever there are changes to multiple subprojects, make individual commits for each subproject.
This avoids commit message repetition and also ensures that the commits make sense on their own
when pushed back to the original repositories.

Rebasing after a subtree pull doesn't work. On rebase git looses track of `--prefix` which will lead
to a mess in the project root.

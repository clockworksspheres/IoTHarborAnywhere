# How the Oracle docker-images submodule was linked to this repo -

Linking external git repos to a current repo can provide much better management of an external project or library.  Linking an external resourcem, rather than copying that external resource into a current project means that one doesn't have to manually syncrhonize the entire external maintenance, security and feature updates into your current project, and which version or branch of the external code/library that the current project uses can be entirely maintained in the current project.


## From [stackoverflow](https://stackoverflow.com/questions/7813030/how-can-i-have-linked-dependencies-in-a-git-repo)

Note: comments on the question and answer not shown here, but may prove valuable.

### question asked Oct 18 '11 at 20:06 by [Lea Verou](https://stackoverflow.com/users/90826/lea-verou)

In my scripts, I often use libraries (mine or others') that have their own repos. I don't want to duplicate those in my repo and get stuck with updating them every time a new version comes out. However, when somebody clones the repo, it should still work locally and not have broken links.

Any ideas about what I could do?


### answer Oct 18 '11 at 20:29, by user [Emily](https://stackoverflow.com/users/105938/emily)

You can do this with submodules in git. In your repository, do:

```
git submodule add path_to_repo path_where_you_want_it
```

So, if the library's repository had a URL of git://github.com/example/some_lib.git and you wanted it at lib/some_lib in your project, you'd enter:

```
git submodule add git://github.com/example/some_lib.git lib/some_lib
```

Note that this needs to be done from the top-level directory in your repository. So don't cd into the directory where you're putting it first.

After you add a submodule, or whenever someone does a fresh checkout of your repository, you'll need to do:

```
git submodule init
git submodule update
```

And then all submodules you've added will be checked out at the same revision you have.

When you want to update to a newer version of one of the libraries, cd into the submodule and pull:

```
cd lib/some_lib
git pull
```

Then, when you do a git status you should see lib/somelib listed in the modified section. Add that file, commit, and you're up to date. When a collaborator pulls that commit into their repository, they'll see lib/somelib as modified until they run git submodule update again.


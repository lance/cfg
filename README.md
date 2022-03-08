# cfg
Use this repository to manage your shell, git and other configuration files.

NOTE: If you use it to manage things like your `.ssh` directory, be sure to avoid making the repository public!

## Installing
- `git clone --bare https://github.com/lance/cfg $HOME/.cfg`

When cloned this way, repository is a "bare" git repository, meaning that the work tree must be configured in order to be used. Do this using an alias. I like to use `dotfiles` since that's the conceptual purpose of all of this - to manage your dotfiles. Set the alias like this.

```
alias dotfiles='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME
```
asd
You'll probably want to add this to your `.zshrc` or other shell initialization script so you don't have to do this every time you mess with your dotfiles.

If you want the `git` command to ignore your local files that are not already in the repository, you can configure that setting with the following command. This way, you don't have to explicitly add random stuff to your `.gitignore` file.

```
dotfiles config --local status.showUntrackedFiles no
```

## Roll Your Own

If you don't want to start with this repository, and just want to do your own thing, you can do the following.

```
git init --bare $HOME/.cfg # create a new bare repository in the ~/.cfg directory
```

Then create the alias as above, and configure `dotfiles` to show untracked files or not, depending on your preference.

## Configure your remote

Whether you have rolled your own, or you are using a clone of this repo, you'll of course want a remote on github or gitlab or whatever. Create the remote on your github or gitlab account, then add it to your local settings.

```
dotfiles remote add origin https://github.com/<account>/cfg
```

Then you can use your local home directory as you would any other git repo with the `dotfiles` alias. For example, here I am updating the contents of my `.gitignore` file.

```
❯ pwd
/Users/lball

~

❯ vi .gitignore

~ took 20s
❯ dotfiles status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   .gitignore

no changes added to commit (use "git add" and/or "git commit -a")

~
❯ dotfiles commit -am "Update gitignore - add ./bin"
[main 5917af68] Update gitignore - add ./bin
 1 file changed, 3 insertions(+)

~
❯ dotfiles push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 10 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 735 bytes | 735.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To github.com:lance/.confg.git
   79c2bfdf..5917af68  main -> main

~
❯ dotfiles status
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean

~
```

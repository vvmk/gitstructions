# What to do if you have to use Git during a test

**EDIT: to pull down all remote  branches at once:** `git fetch --all`
 
###  Don't panic. 
Git is awesome and is designed to PROTECT your work. It is a tool to make your life as a creator easier.
###  Be cool.
* Let's say the **repo**sitory for the test is called `Assessment2`, and it was posted by the user `zipcoder`. That means it lives at the url `https://github.com/zipcoder/Assessment2`.

* Fork the repo from github so you can have your own separate copy to modify as you see fit. It would be uncool if you could just push changes to someone else's repo, right?

* After you click `Fork` you should be taken to the location of your new copy. Notice the url is now: https://github.com/**YOUR_USERNAME**/Assessment2

* Now you have your own copy of the repo to do with as you please, and the original owner of the repo (zipcoder) can sleep at night without fear of you changing any of their work. Cool, right?

###  Set yourself up for success.
Now that you have your own personal copy, you're free to change it however you want. Head to your Terminal and **cd** into the directory where you'd like the files to be, then tell `git` to `clone` your repository. 

`git clone https://github.com/yourusername/Assessment2i.git`

* What git did for you there is:
	+ created a new directory
	+ downloaded your fork into it
	+ set the remote url to the keyword `origin` so you don't have to type the whole thing again
	+ started you out on a `branch` called `master`
	
* That would have been really annoying to do on your own, but git did it for you with one command!

###  Cover your ass.
* At this point you could start the usual cycle:
	+ make changes (write code)
	+ stage those changes to be committed (git add *changed_files*)
	+ commit those changes (git commit -m "actually describe your changes")
	+ (repeat as many times as you want)
	+ [eventually] push all those commits back up to the remote version of your repo

 But what if one of the instructors decides they want to change something during the test? If they make the change in their repo, will your fork automatically be changed to reflect the update? 

**No. That would be uncool. You made a new fork and it belongs to you.** Even though 'zipcoder' is the original author, they **should not** and **do not** have permission to change your code without your express consent. 

In this case, of course you would want the updated version. There are a couple things you can do ahead of time that might save you some grief later.
	
### 1. Keep the `master` branch clean. 
Only make commits on `master` if you feel like you're done with the code you're committing. Pretend like committing code to `master` is the last time you'll be able to change it before its graded. That's not true, of course, but its a good habit to get into.

Fortunately `master` is just the first branch you start with. Kinda like the trunk of a tree. You can make as many as you want and call them whatever you want. Furthermore, when you are working and adding and committing on one branch, the others are still exactly the same as you left them. 

Make a new branch any time:  

`git branch development`  
	
Sweet, look at the list of branches:  

`git branch`

You should see something like

  development  
* master  

 Now there are two branches, `master` and the new one `development`. The * is next to your current branch. **No one will judge you for how often you check which branch you're on.** Its like checking the fridge to see if you need milk before heading to the grocery store. It takes a couple extra seconds, but could save you A LOT of heartache.

Time to check out the new branch.

`git checkout development` 

See what I did there? Calling `git branch` again should show you the star next to `development`. This new branch is **exactly the same as the branch from which you created it**. If you were following along exactly, that means you were in your `master` branch, so `development` is now exactly the same. The benefit is that now you can work and commit changes to to this branch while keeping `master` clean and shiny.

Let's say you do some work and make a few commits on `development` and you want to add them to master. **Make sure any changes you've made since the last commit are committed**, then switch back to `master`  

`git checkout master`  

and `merge` the `development` branch  

`git merge development` 

Everything should go smoothly since `development` was originally an exact copy of `master`  and you're the only one working on your local files. Now you can push your local version of `master` back up to `origin` if you want (git push origin master)
  
		If you're still afraid you might break something, you can always 
		add/commit your changes, switch to master, then make a new 
		branch from there called fakemaster or whatever. Switch into 
		the fakemaster and try merging. Any havoc you cause is limited 
		to that new branch and master is still clean.

### 2. Don't change any of the 'test' files.

Merge conflicts are not as scary as they seem, but right now it's better to just avoid them. If you don't make changes to any file under the /src/test/... directory, there won't be any merge conflicts. Period.

If you want to write some extra tests, creating your own test files is totally fine. You can create them in the same place as usual without fear of merge conflicts. 

### 3. Prepare to pull the changes

If you keep master clean, you always have a safe point to go back to. If you don't change any of the original unit test files, there won't be any merge conflicts. Almost done, one more thing to set up ahead of time...how to actually pull down the changes.

Remember when you made a local `clone` of your remote repo? Git stored that ugly url (https://github.com/**yourusername**/Assessment2) behind an easy-to-remember keyword called `origin`. Now whenever you want to `pull` from or `push` to your remote repo (on gitHub) you just have to say `origin`. But if the test cases (or anything else) are updated, that's not going to happen at `origin`. Its going to happen at a different `remote` repo: https://github.com/**zipcoder**/Assessment2  

That's an easy fix: `add` the other `remote` address under a different name. zipcoder seems appropriate (these keywords are case sensitive):

`git remote add zipcoder https://github.com/zipcoder/Assessment2i.git`  

Now we still have our own version of the repo at `origin` but we can also pull down any new changes by using the keyword `zipcoder` instead. 

When you're ready, add/commit your changes, then switch to `master`. Pull the changes the same way you always do, except specifying the new `zipcoder` remote instead of the usual `origin` 

`git pull zipcoder master`  

Assuming no typos, your local `master` branch should now have the updated files. If you were in the middle of something on a different branch, you will have to switch back to that branch and  

 `git merge master`  

if you want the new changes to show up there too.  

### 4. Carry on.

Business as usual. The changes you pulled down from the `zipcoder` remote repo will be incorporated into your code locally, and will be included with everything else when you push to your own `origin` remote repo with `git push origin master`.

### Reminder: 
* Check your branch often. When you use commands like `pull` and `merge` and `commit`, the target branch for these commands is **the branch you are currently on**. For example, if you are on a branch called `dev`, you can still `git pull origin master`, but be aware that you are pulling down whatever is on the `master` branch of the repo at `origin` and merging that into your local `dev` branch. That's totally ok, as long as that's what you mean to do. The same goes for `push`. If you run `git push origin master` while your `dev` branch is selected, you will push your local version of `dev` to the `remote` version of `master`. If you want to `push` to a different branch than `master`, just change the branch name: `git push origin dev`  
  
  
glhf  
-v

# Source Control

**Use git.**

**Work from your <a title="or master">`main`</a> branch.**

**Use `squash` merging to keep a straight-line branch in your history.**

**Prefer more, smaller changes over fewer massive changes.  Presentation, business logic and data layer are good boundaries for dividing commits for a particular feature.**

**Build and deploy from your `main` branch.**

**Avoid modules if at all possible.**

Linus gave us git and it has taken over the source control world.
Embrace git.  There are literally thousands of commands.  I mainly use the ones I show here.  They work on any command prompt or shell.  Sometimes I have to look up a new command because I borked something.  Really though this is it.

|Command|What it does|
|---|---|
|`git clone https://github.com/DonFrazier/HowToDoCSharpRight.git`|Get all the files from the primary server location.|
|`git checkout -b users/don/nnnn_description`|Start working on issue `nnnn`.  Cloning is instant and just updates some pointers in the git indexes on your machine.  It is not like TFS CLONE at all.|
|`git add .`|Tell git I am ready to send everything to the primary server.|
|`git status`|Ask git what has changed on my local copy of the files|
|`git add somefile`|Explictly add a file that the command above didn't add.   I don't usually worry about why.|
|`git commit -m 'what I did'`|Send my changes to the primary server.|
|`git checkout master`|Get ready for my next change.|
|`git pull --prune`|Get the latest files from the primary server|
|`git merge someOtherBranch`|Merge another set of changes into my feature branch.  Often this requires resolving merge conflicts.  I use Visual Studio to resolve merge conflicts.|

My coding [tool](./tooling.md) of choice is Visual Studio.  I sometimes use its git functions instead of these commands.  Under the hood Visual Studio is sending these same commands so I just let it do some of the grunt work.

I clean up my local branches using `gitk --all`.  It works on every environment and gives me nice enough visualization to see what branches I need to delete locally.  It does a lot more than that but this is my primary local cleanup tool.

Before Visual Studio supported partial staging of files I used to use `git-gui` if I only wanted to send a portion a file change to the primary server.  Now I can do that in Visual Studio so I rarely use `git-gui` these days.

I use Visual Studio to resolve conflicts.  Most of the time its 3-way merge UI helps me get it right.  It can be difficult to use when there are many conflicting changes though.  I try to avoid making big changes.

On the server my preference is to use a squash merge when completing a pull request.  Since I tend to commit work in progress often, there are often many commits I push to cloud to avoid losing local work.  The squash turns them into a single commit so the git history shows a nice straight line of commits from the repo creation to now.

Generally features span presentation, business logic and the data layer of your application.  To move quickly these layers are loosely coupled and follow strict rules.  Presentation calls the business layer.  The business layer processes the request, reading or write to the data layer.  Nowadays these layers may be separated by one or more networks and not be on the same physical machine.

It is ok to deliver parts of the feature incrementally.  Safely hidden until ready, you can work on the layers in any order.  The data layer is what persists even when no one is using the application so I like to start there.  Invariably as the business motions are fleshed out, additional properties appears that were not part of the original data model.  That's ok.   The data model can often be changed incrementally with some of the business logic and still be a relatively small change for your peer review.

The User Interface (or presentation layer) is what the user sees.  Nowadays the UI may be in a browser and all of the actions are network calls to read and write data.

I think these make good boundaries and order is logical.  Until there is something for the user, the business logic and data layer are just idling quietly.  There are often subject matter experts (SMEs) on a team that will concentrate on one or more of these parts of your code review.  Separating changes along these boundaries helps to ensure your peer reviews are getting comments from the peers whose comments probably offer the most value.

If you are using multiple branches before you get to shipping code, I ask "Why?" For most apps I work on, incremental features are added and deployed daily, often by multiple developers.  We call that `moving at web speed`.

If you have a humongous code base modules are one solution.  My personal belief is if you segregate your code you can build separate .dll instead of modules, keep your contracts between file boundaries clean and use the linker to assemble your final package into an .exe or similar package.

[Back](./motivation.md)  [Next](./tooling.md)
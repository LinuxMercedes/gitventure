General Idea
============

Each branch of this repository is a room in the adventure. Rooms contain a README.md describing the room and submodules offering various actions that take you to other rooms. 

First off, we're going to make each branch with its own root because they shouldn't share any history. 
(I guess if you want to build off one room with another, they would share history and that should be fine.)

Then, we'll make a bunch of git submodules pointing at various branches of this repo, depending on what we want to let people do. 

Instructions
============

First off, make yourself a new room:
```
git checkout --orphan <unique room name>
```

Now, git still leaves a bunch of stuff in the repo even after you've made an orphan branch. 
You'll have to remove any submodule directories with `rm -r <submodule directory name>`. 
Then, remove any remaining staged files with `git rm -rf *`. 

At this point, you should have a nice empty directory. This is good. 
Make a `README.md` and put your stuff for the room in it. Add and commit. 

Now, let's add some actions. You can add actions whenever you feel like it as long as the branch they're taking you to exists. 
Because submodules weren't meant to be used like this, we're going to have to do some trickery to prevent name collisions. 

To add an action, do
```
git submodule add -b <destination room> --name <this room>--<destination room> <https clone url for this repo> <action name>
```

For example, if we're in `scary-dungeon` and want to go to `boss-level` with the action `go-through-the-scary-door`, we'd do:
```
git submodule add -b boss-level --name scary-dungeon--boss-level https://github.com/LinuxMercedes/gitventure.git go-through-the-scary-door
```

Once you've done this, make sure to commit your changes! Git should already stage the submodule changes for you. 

Finally, let's push this new branch to the repo: `git push -u origin <this-room>` 

Now, you'll probably want to add some way to get to your new room. 
Do that by checking out whichevever room branch people can come from and adding a submodule to your new room, just like you did with the actions above. 

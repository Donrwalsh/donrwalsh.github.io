## Resume

I aim to improve upon how I manage my resume.

I created a new page for this, aptly named resume. I won't advertise it yet, but it's available at /resume. It should just say 'resume' for now.

The plan is to link multiple resumes here. Split on frontend, backend and leadership to start. Have three different easily accessible resumes available for download depending on the role I'm looking for at the time.

How best to catalogue and store reminders for work done in the past? Spend some time going through hand-written notes to capture important items that I can't recall.

Consider shifting around format? I still like the overall structure that I'm using right now.

Start with a technology inventory for each job, should be a good way to get the ball rolling!

# donrwalsh.github.io

## TODO:

- This readme is a bit of a mess and could stand to be organized better.
  - (this includes callouts to the other repos that are related to this one which to the best of my knowledge is not managed anywhere except in my memory.)

## Includes

- Bootstrap
- Bootstrap icons
- jQuery
- MathJax
- Rouge

## Breadcrumbs

https://help.github.com/en/github/working-with-github-pages

Installed Ruby (https://rubyinstaller.org/)

Installed Bundler (https://bundler.io/)

Got things started with https://jekyllrb.com/docs/step-by-step/01-setup/

`>jekyll serve` to run server.

## Notes

Adding content https://help.github.com/en/github/working-with-github-pages/adding-content-to-your-github-pages-site-using-jekyll

Jekyll documentation https://jekyllrb.com/docs/

https://jekyllrb.com/docs/step-by-step/01-setup/

Favicon sourced from: https://gauger.io/fonticon/

https://stackoverflow.com/questions/33113945/can-jekyll-use-a-config-file-from-a-different-repo <- Didn't have a ton of luck trying this out.

It would be swell to share assets such as templates between different repos so I can link out to CLRS stuff without pulling it in here.

^ This doesn't seem to be in the cards. I am going to roll my CLRS repo into this repo instead.

This looks cool for a readme template: https://github.com/othneildrew/Best-README-Template/blob/master/README.md

Syntax highlighting: https://mycyberuniverse.com/syntax-highlighting-jekyll.html

Matching with Github Pages:

Add Gemfile with `bundle init`. Change version to match github.

`bundle install` and then `bundle exec jekyll serve` to generate files the same way pages does.

Use the `--drafts` command-line argument to be able to review drafts locally.

## Setting up on Windows:

Tried running out of the box and it didn't work, so I went to the familiar installation guide and followed the Windows steps: https://jekyllrb.com/docs/installation/windows/. Grabbed the latest version of Ruby with the Devkit (3.2.2-1 (x64)) and confirmed that `>ruby` and `>gem` commands work in a fresh command prompt. `>jekyll` commands don't work, so let's proceed with the instructions. There's a command to install jekyll so I run it: `gem install jekyll bundler`. Now I see `jekyll 4.3.2` when I run `>jekyll -v`.

`>jekyll serve` didn't work, so I ran the `>bundle init` (unneccessary) and `>bundle install` (crucial) and then ran the `>bundle exec jekyll serve` command which failed.

Fussing around with this: https://stackoverflow.com/questions/65989040/bundle-exec-jekyll-serve-cannot-load-such-file but the top-most instructions don't get me anywhere. So I moved my way through this and then ultimately discarded it when none of the stuff was getting me anywhere. Found this next: https://stackoverflow.com/questions/70859127/bundle-exec-jekyll-serve-causes-loaderror which seems promising.

I outright ran `bundle add rexml` and then `bundle install` and then upon running the command, I'm no longer seeing the old error and am seeing another one. Success!

This next message is familiar to me. Has to do with the latest version of Ruby not being compatible with something that I'm using. Could've sworn I made notes on this but I guess not. Gonna step away and then pick up from here when I return.

I want RVM to make this easier: https://rvm.io/rvm/install. Oook, so this is a quagmire. The only way to use RVM on windows is by way of WSL which I'll probably want at some point, but not right now. _Especially_ since all I'm trying to do is get a version manager (some spicy snark in a github comment about this) so I'm just going to uninstall the latest version of ruby I grabbed and then manually install 2.7.8-1. I am the Ruby Version Mananger.

Cool, so now I'm getting a failure to find some file/directory when I try to run any `bundle` commands. https://www.jessesquires.com/blog/2020/11/28/how-to-fix-ruby-bundler-errors-on-nearlyfreespeech/ Seems that bundler is still referencing the old version of Ruby after the upgrade. Makes sense. So I re-ran `>gem install bundler` and then the `>bundle install` followed by `>bundle exec jekyll serve` and we are running!

So overall, I needed to install the right version of Ruby (2.7.8-1-x64) and then run `>bundle install` followed by `>bundle exec jekyll serve` and boom. So that means the stuff above about adding `rexml` and `webrick` appears to be unimportant and so I've removed them. Ahh, I bet that I'll find instructions on how to deal with this in a different repo since this is the one that doesn't really get any action.

Minor thing: An even better command to run is `RUBYOPT='W0' bundle exec jekyll serve` which suppresses the constant warning messages about using the `last` argument as keyword parameters is deprecated. I believe this warning message is at the language level because I only use that as a keyword in one place and that's over on the CLRS side of things, so I suspect trying to 'resolve' this isn't going to do much at all.

## Environment Differences

So I'm working in this space right now because it's an obvious QoL in my face that I can hit the ground running on. I'm dropping notes here because this readme is kinda just a running stream of consciousness right now and will need to be tidied later. So actually, let's make a todo for that. Cool, added a TODO section.

Ok, so env differences. First off, there is no visual difference between dev and prod. So I changed the banner color when we are working with a local environment to make it very obvious. Another thing is that the links are standardized which means they always point to the prod version of things (because that's how I arranged it). This is an easy fix, and the environment that the app is running on is easily apparent and checkable, so I added some logic to switch which link is being used based on that environment.

In order for the link switching to work, I need to run things locally a little different. For example, I am running both the core donrwalsh.github.io and CLRS locally right now using the current run command which is `RUBYOPT="W0" bundle exec jekyll serve` and it is the same for both. This means that both apps are running on port 4000, which technically shouldn't be a problem because despite this there are no overlaps in URLs. Even so, only the first one that is running will actually show up locally. Unclear why local can't map to a single port when prod does it just fine, but that's alright because with what I'm working on here I can simply establish a slightly different running pattern for locally by assigning ports to each of the sub-repos and having the local dev server map to those locations rather than the prod locations (or an equivalent construction of a URL based on prod principles). I will probably set this workspace up with restore terminals to better take advantage of these growing run commands.

### Restore Terminals

This ended up being a bit of a hassle. The instructions (https://marketplace.visualstudio.com/items?itemName=EthanSK.restore-terminals) are detailed, but there is a big gap in my opinion on the specificity of what actually needs to happen. The settings themselves go in a configuration file, which in normal circumstances should be available in the `.vscode` directory, but that doesn't exist for a workspace. I know from experience that the settings go in the workspace file, but there's no indication that this is even possible just based on the quick intro and then complete absence of content around this plugin. Indeed, VScode has a native way of doing this now, but I'm stubborn and am going to work this.

Anyway, it wound up being that I need to prefix the addition of these settings in the workspace file with a `"settings":` so that it is clear that what I'm listing off are settings and not something else. I also had to append `restoreTerminals.~` to the RT-specific settings. This seems to work just fine, and I was even able to move the workspace file into the repo itself and get it working. The CWD of the commands that are run via the file is based on the location of the workspace file itself, so moving it inside the donrwalsh.github.io repo means that the commands (and folder paths, for that matter) needed to be updated in kind.

### Fontawesome -> Bootstrap Icons

For the past two months, I've been getting warning emails from fontawesome that I'm reaching some limit on the free account that I have with them. Based on the analytics I setup, this site gets a steady stream of traffic and I want my visitors to see icons every time. Managing a subscription for (admittedly great) icons is a bit too involved for my tastes, so I decided to switch to Bootstrap Icons which I've had success with on a separate project. I was able to do a nearly one-to-one transition with this, save for the goodreads icon which bootstrap doesn't recognize for whatever reason. I went with a generic book instead and do not plan to lose any sleep on this. Otherwise, I believe I have eradicated all presence of fontawesome in this project and will be keeping my eyes peeled for anything I missed.

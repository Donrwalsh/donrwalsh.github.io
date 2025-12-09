## Resume

I aim to improve upon how I manage my resume.

I created a new page for this, aptly named resume. I won't advertise it yet, but it's available at /resume. It should just say 'resume' for now.

The plan is to link multiple resumes here. Split on frontend, backend and leadership to start. Have three different easily accessible resumes available for download depending on the role I'm looking for at the time.

How best to catalogue and store reminders for work done in the past? Spend some time going through hand-written notes to capture important items that I can't recall.

Consider shifting around format? I still like the overall structure that I'm using right now.

Start with a technology inventory for each job, should be a good way to get the ball rolling!

### 11/24/25

To start with I'm going to make a `resume` folder. I've found it very useful to have this repo serve as a sort of quick-access for helpful files so I'm going to continue that and expand it a bit. The existing `resume source` folder goes away and moves to my new folder. I store the font files here because on fresh machines OpenOffice needs them, so they get their own folder. Then I made `sources` for my resume source files, of which there is one. On the frontend the only resume-related thing that gets exposed is the pdf itself which I haven't touched yet.

I don't think I'll be using the original resume for much longer, but I want to at least make a few changes to it right now. Specifically adding back months to the date ranges and adjusting the location to be Brooklyn Center. Ah yes, I'm also missing Cogency Global from this resume so I'm going to add that now. Musn't forget to extend the red lines to match the new date lengths!

Ah yes, Open Office crashes every time I try to export to pdf. I remember that I need to use print to pdf to get it to work for some reason. With that, I'm going to replace the top level resume.pdf with my latest and commit these updates. That change should be the only impactful change, everything else is just tidying.

Watching the automated build stuff makes me think I should write up how that works at some point during this process. Note that the printed pdf carries the filename of the source file that it printed from. (visible in the online pdf viewer and likely different than the actual file name that is being shown)

Alright, let's tear it apart. I'm going to focus on the left-hand sidebar. I like the Education section and I don't think I want to change a thing about it right now. But the Technical Experience section is a mess. Actually I think I want to do this in a separate file.

So I took a stab at listing out all of my tech experience by tech and then bullet-point listing each of the jobs or projects that I used the tech on. This is a good start, and I thought of a better way to arrange the data on my resume so I made an update with that in mind. Now I'm grouping tech in 3 buckets: 5+ yoe, 2-5 yoe and <2 yoe. I like it better than the big pile of languages so I'm gonna roll with that for the time being.

I'm having this pretty cool idea for how to rearrange the homepage of my site. I'm imagining a timeline-focused version of my tech experience. Also some Testimonials would be pretty cool. I'm going to plan to add these but in order to make them pretty it feels necessary to upgrade Bootstrap since I'm pretty far behind there. I worked a bit today on getting Bootstrap up to 5.3 for this project and I believe I've gotten the main issues handled, especially since this project is pretty much just a single page.

### 11/25/25

Today I'm going to work on the timeline. I have a few ideas of how this might look, but mostly I want to get some copy in place to replace the existing copy that has been on my homepage for years now. It's so outdated! What I'm thinking is to work with 4 different regions. I'll probably use the resume placeholder page for this. Though, I should rename that.

Alrighty, so I made a new page `timeline.html` and I put in some sections with the headers that I chose. I'm not the biggest fan of using accordions, but I figure this is a good spot to place some copy as I come up with it. I spent a little time tweaking the core accordion structure so it is something that I'm happy to leave as is and work on. I think I'll commit this for now and pivot to the favicon because I'm not the biggest fan of the green smiley face anymore. . .

Ooh, so I think I'm going to use the cross-stitch I made since it's a circular image anyway and it's something that means a lot to me. It's just a favicon anyway, so doubtful that people will notice it all that much. Could be fun to do some sort of callout on what it is when it comes up anyway.

To make it, I started with the image from my google photos and opened it in Paint. It's pretty simple to remove the background as Paint provides a button that does just that. From there I needed to save it as a .png (specifically going into Layers and removing the white background layer that was showing instead of transparency) and then I used an online converter that spits out a handful of favicon files. I generally only use the `.ico` file but I'm curious what all these other files are for. I don't think I'll fuss with that much right now since I can easily retrace these steps at a later time.

I've had that turtle image on my homepage for years but I always felt a little odd about it. I ripped it from Wikipedia (I think) and didn't put much thought into it. After swapping around my favicon I figure that this is also a good opportunity to change that picture, so I swapped it out with the cross-stitch mountains too. Honestly, that feels like a really nice thing to have as the first image many people see when looking me up.

I badly want to rip out my copy on the homepage since it is so outdated, but I'm going to leave it there for now with a note describing how outdated it is. That'll do nicely for now I think. I enhanced some styling while I was at it.

Spacing on the page and with the icons was a little wonky. I adjusted it by switching back to just using `.container` rather than `.container-fluid`

Spent a little time on playing around with a quote block. I'm not sure where they go yet, but I have this idea in my brain of having quotes scattered throughout the site of testimonials about me, sort of a 'soft-reference' kind of thing. I haven't sourced any quotes, except I do have one that I plan to include as decoration amongst all the professional ones. Played around a bit with having an image, but I'm not sure that's a great idea. In any case, I put some styling together for the quote and I moved it into its own file since I'm not sold on this being perm just yet. Reminds me that the styling scheme I have setup shares `main.scss` with CLRS but not other ones. Nope, nevermind it pulls everything in haha. So I guess I don't need to worry too much about breaking everything out? I might just do that next since it's bothering me how weirdly the styling is arranged.

### 11/26/25

Woke up this morning by playing around with styling. I established a `clrs.scss` file since that's where a lot of the styling is used and it seemed helpful to break it out into its own file. I've still got `main.scss` for content that's structural or shared between the homepage and clrs and then `accordion.scss` and `quotes.scss` as isolated style files for stuff that I'm tinkering with. I suppressed the annoying lint rule that expects a left curly bracket in `styles.scss` by making a dummy style rule that does nothing but satisfies the requirement since I couldn't drum up a way to suppress it outright. I'm fine with this and it kills the annoying red squiggly in my IDE so that's swell. Added a quick note to the readme which satisfies the TODO, but mostly I just need more content in the README to feel satisfied about it.

(Needed to do a brief update to CLRS github actions for it to run) I changed a class from camelCase to kebab-case and inadvertently broke the 'random assignment' functionality that I've got on the main CLRS page. I can fix this up, but it's still using jQuery which isn't really necessary in this day and age, so I think I'll play around with retaining that functionality without needing to pull in jQuery. I guess I'll first double-check to see if I'm using it anywhere else. . . Ok, score this is the only place. This seems worth working on but if I'm being really honest I'm just procrastinating on doing resume stuff haha.

`random-assignment` is more appropriate as an id than a class. So I got this working by adjusting some of the jQuery syntax I was using to use vanilla javascript. This is pretty cool, because now I don't need jQuery at all on this project but it's also just a good exercise of translating what's in my brain into what's possible with vanilla JavaScript these days. Pretty sweet.

### 11/27/25

Little bit of morning work finalizing some updates to my resume I worked on yesterday. Now I'm off to have some delicious grub! Happy Thanksgiving!

### 12/1/25

Alrighty, I'm here to shake off the Thanksgiving. Grabbing the top TODO for now so let's look into Github Actions. Looks like at the free tier I'm dealing with 2,000 build minutes monthly and 500MB artifact storage cumulative. Last month I had 130 total minutes for 25 total runs. Sorta high, but I'm not gonna hit the limits for a while.

While playing around with this, I noticed that CLRS was running two sets of GitHub Actions on every run: one was the workflow defined by the project-contained yaml file, but the other was the default github pages build action at the repo level. I messed with settings a bit and turned off the automatic run and then upon a commit I see that only one workflow is running, nice. Also seems to be happening on this Repo, so let's mess with that.

Wrote a new intro for the main page.

### 12/2/25

Today I posted a new CLRS solution for the first time in a long while. I'm working on brushing up on my data structures, so I chose chapter 10 as my spot to start. It was quick to review the work I'd already done on linked lists, and the problem I tackled (10.2-4) was pretty straightforward. Great choice for getting my feet wet once again!

Made a few minor adjustments to styling because I noticed an inconsistency in how links were being underlined. Now links on the main CLRS page and previous/next links within a solution should only show underline during hover.

### 12/3/25

Working on some linked list exercises this morning and took another crack at the homepage copy.

### 12/4/25

I discovered that I am 2 versions behind on Mathjax. [Version 3](https://docs.mathjax.org/en/latest/upgrading/v2.html) is a full rewrite (meaning it isn't backwards compatible) and [Version 4](https://docs.mathjax.org/en/latest/upgrading/v3.html) has some fancy table decorations that I want to use for exercise 10.3-1. Upgrading looks to be no small task, so I'm going to park the idea for now and potentially swing back around later to do it. I'd need to pretty much vet every single solution and I'm pretty pleased with how v2.75 performs right now so I'm not looking to switch just yet.

Chatting with an old colleague, I made a version of my resume that's data-focused. Didn't require much changes, but I'm also listening to feedback on it so I may make some more adjustments here soon.

### 12/5/25

Not much exciting to report. Chatting with some recruiters and doing initial tech screens. I'm getting a little tired of linked lists though, might pivot to hash tables soon.

### 12/9/25

This weekend I had an interesting idea that I'm playing around with this week. I'm a big fan of the Final Fantasy series and I recently picked up a Steam Deck and the entire mainline game library. I've since been picking away at the games and I figured it'd be fun to track my progress through this task on a sub-page of this site! Steam has an API that I can use to obtain details about my progress through games (via achievements), but this requires an API key so I can't just make the API calls in the javascript of my site. Instead, I opted to set them up running through Github Actions which allows for obfuscating secret information.

The way I've got this setup is the github action workflow that I use to create my github pages now performs a suite of API calls to grab user stats and game schemas for each of the games that I've designated as a member of 'the list'. The response to these calls are combined together into two different json files that are placed in the `./_data` folder prior to building the site. Then the page that works with this data `ff.html` is built as though those json files are already present and boom, I have a working page that does what I want and my API key is safe and secure. Pretty cool, and only took me a couple of hours to put together! Shout-out to Github Actions for being easy to use.

Now I'm messing around with the different data payloads and manipulating them to show the data I want. So far, I've had to deal with pretty odd naming conventions for the games but that was solved with a simple mapping yaml file. Other than that it's mostly been a matter of cozying up with the structure of the data and getting it to display things the way I want them to be displayed. I've got some work that I didn't commit from yesterday that has the page show a list of (proper) game names and then a readout of achievements completed out of total achievements. Thinking maybe some accordion structure from here?

Pulled icons from https://www.steamgriddb.com/. Copyright concerns? I used an accordion template to get the ball rolling and the chevrons behave oddly. Otherwise, what I built here has all the core functionality that I want for this page. Jekyll logic is goofy, but it flows once you think about it the right ways.

## TODO:

- [ ] Front page image is too large. Didn't load once for me, awkwardly.
- [x] Clean up Github Action files (generic comments still linger)
- [x] Approach styling organization. Document how this is done in the README.
- [x] I'm getting an annoying syntax error on styles.scss but it's definitely valid. Could look into that?
- [x] Links on CLRS are odd. Main nav page links don't underline even on hover and forward/back links on solutions are always underlined.
- [ ] Chapter/Card specific progress indicators for CLRS would be cool and fun to build.

## Stretch TODO:

- [ ] Wouldn't mind updating my branch names to be `main` instead of `master`.
- [ ] I set this workspace up a long time ago on this machine. Could be helpful to document all the pieces that go into it and make it easier to set up again. Containerized workspace? Maybe that's a bit much, but I at least have my laptop to consider.
- [ ] Are there ways that I can enhance my usage of Github Actions so it's doing more for me? It is pretty basic right now.
- [ ] Mathjax upgrade from v2.75 to 3 or 4.

## Other TODO:

- [ ] WalkCCC has an incorrect solution on 10.2-5 because it assumes a sentinel variable. Could do a PR for that.

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

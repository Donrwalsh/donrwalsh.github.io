# donrwalsh.github.io

## Includes

- Bootstrap
- Fontawesome
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

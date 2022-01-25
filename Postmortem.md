# Result of ~2h timebox: build unsuccessful

## Original plan

* Get the thing running
* Implement some responsive UI.
  * Specifically, the game page captions ("Welcome, Player" / "Play comp" / "Start game" / "Your turn") consume a lot of real estate at mobile screen sizes.
  * On my phone at least, only the top third or so of the game board is visible without scrolling.
  * I was going to wrap the welcome and "Play" text in a component to collapse it at smaller screen sizes, and rejig the "Start game" / "Your turn" text to be more vertically compact.
* Test on my phone by using ngrok to make a temporary tunnel from my local dev server to the public internet.

## Problem

* Attempted to build project using
  * Windows 10
  * node 16.13.2 / npm 8.3.2
* Build failed upon attempt to build a SASS binary locally

## Fixes attempted

* Corrected PATH environment variable to detect Python 2 executable first, before Python 3 executable. Successful.
* Next, corrected PATH to detect Visual Studio 2017 flavour of MSBuild first, before 2022 version. Successful.
* SASS build still unsuccessful. Predicted that digging further into the SASS build was likely to be a massive time sink with low probability of success.
* Researched published node-sass releases on npm and github. Found no github listing for the version in question, 3.8. Through reading similar issue reports (esp. https://github.com/sass/node-sass/issues/2133), found a suggestion of a workaround - directly downloading a binary from github (via unpublished link) and manually placing where node-sass would check for it before deciding to build its own. Unsuccessful. Node-sass installation log output did not seem to report that it was even checking for an extant binary. Abandoned this line of enquiry.
* Briefly investigated updating dependencies as minimally as possible. Concluded to be impractical in the time available, given that updating node-sass required updating sass-loader, which required updating webpack, and so on. The required webpack update alone crossed a major breaking change boundary and would have necessitated a complete rewrite of the webpack config files.
* Excised SASS components from build. Copied the built `style.css` from WS/public into react_ws_src/static, and updated the build to copy it into the output directory.
* Able to build this amputee project without error, though CSS rules from `style.css` are not applied properly on the page.

## Roads not travelled

* Setting up a Linux virtual machine or the Windows Subsystem for Linux to attempt building with non-Windows toolchain - judged to be another unjustifiable time sink

## Conclusion

* Upload this documentation as evidence of effort, troubleshooting approach, and so on
* Request alternative challenge?

## Purpose

Investigate the use of Replit to provision single use developer environments that smooth the onboarding of new hunters to the bounties program.

## Scope

sphinx-tribes-frontend

https://replit.com/@skibler/sphinx-tribes-frontend?v=1

## Overall Analysis

I think Replit could work but there are some concerns.

The Good
* Pretty good web IDE, support for linters and LSPs
* Built-in web preview
* Environment customation through standard and open tools (nix and toml
  config)

The Bad
* GitHub integration is weak
* Free plans limited to 20 hours / month is very restrictive for a
  developer that needs an environment like this
* No API for custom integration
* Community forums have been axed

My opinion of Replit is that it's a product that has been positioned for
acquisition more so than to deliver a high quality development experience.

Given the features and capabilities I can identify in Replit here's how
a workflow would have to work.

1. User clicks deep link on bounty or one given to them by assigner
2. User clicks "Remix this app" button in Replit
3. User authenticates with their GitHub account in Replit
4. User clicks "Authorize Replit" in the GitHub OAuth page
5. User completes email verification of Replit account
6. User clicks "Remix this app" again
7. User has a running Sphinx Frontend
8. User forks sphinx-tribes-frontend on GitHub
9. User configures their fork as a new Git remote in Replit
10. User can now develop and push changes to branches on their fork

## Desired Features

__Can a user quickly launch a developer environment based on the latest master branch from a Deep Link (i.e. we have a preset link in the Bounty that creates the env).__

Yes. Kind of.

Public Replit projects can share links to quickly import the
project to a new Replit account.

1. Click deep link
2. Click "Remix this app" button in Replit project landing page
3. Click authenticate with GitHub
4. Click "Authorize Replit" in GitHub OAuth page
5. Verify email
6. Click remix this app again (I think)

__Can this developer environment be preconfigured with all dependancies already installed.__

Yes.

Replit supports configuration through two different files in the
repository root.

_replit.nix_ to define system dependencies (specific version of NodeJS,
dependencies for compiling etc)

_.replit_  app behavior; what command the "Run" button runs, environment variables etc

__Can we customise this image or run a script on start up to setup the app to use the staging environment as the backend (outlined in the readme, but ideally this would be automated)__

Yes.

The sphinx-tribes-frontend can be configured through Environment
Variable to use the staging environment for the backend and Replit
supports defining Environment Variables in the .replit configuration
file.

__Can we automate generation of a feature fork - if possible can this be defined in a deeplink (e.g. branch = featureID_randomID)?__

No, I don't think so.

Not directly/natively with out-of-the-box Replit features. This may be
possible with an integration developed that sits in between the Sphinx
app and Replit but it still might not be possible because it appears
that their API was discontinued in 2022.

I tried passing a branch name through an arbitrary HTTP query parameter
in the public app share link and while it carried through the sign up process
pretty far there is no documented way to access that information within
the project.

Furthermore, if a user loads an app into the Repl from a public GitHub
repo, there is no ability to fork on GitHub from WITHIN Replit. The user
would have to fork on GitHub, then go into Replit and configure their
fork as a new remote repository.

__Can users run these developer environments for free on demand?__

Yes but severe limitation.

Limited to 1200 minutes (20 hours) per month.

Start plan resources are limited to 1vCPU / 2GB RAM / 2GB storage.

I forgot to stop the first account I tested with and left it running for
a few days and my time was up. I think that's a likely use-pattern for many
bounty hunters.

I was able to compile and run the frontend on this instance size but it
completely maxed out the RAM and CPU. It's unlikely to be a positive
development experience.

With my other GitHub account I found that even after my Repl project
seemed to have been stopped that my development minutes were still consumed.
Perhaps it was still running but if I put myself in an inexperienced
persons shoes I saw the Run button and I couldn't see the app in a webview
tab, so it appeared to be stopped. I would expect to not have used development
time, but the next day my development time was consumed.

__Can we centralise payment for these VMs on a Stakwork account if required?__

Yes.

Replit Teams plan offers centralized billing - contact sales for pricing

Can sponsor seats for Replit Core which is $15/mo and bulk pricing kicks
in at 20 seats.

I don't know how that would work though, probably a discount code or
similar. Which means complexity on Stakwork to manage and distribute.

__Can we submit PRs directly from the Replit front end.__

No

There is no out-of-the-box ability to create PRs. The GitHub integration
is fairly primitive.

It may be possible to build this out using an Extension or a Workflow
but I don't know if the GitHub tokens from the Replit authorization
would be available to make the necessary API requests.

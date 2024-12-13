# Feedback for onboarding process

Intro to confluence docs by Aga was useful
Tip to book 1 on 1s was useful.

How to get PIP_EXTRA_INDEX token from servers. Echo on tailscale.

Setup of .ssh/config I needed this for git pull to work from the servers.
```
Host *
  ForwardAgent yes
```

I find confluence and jira confusing and complicated.
Creating a subtask I can't set it to done I have to transition to under development, in testing etc.
I don't understand what issues are actively worked on in the ID dashboard, only some work seems to be tracked?
I create a sub issue but I don't have permission to delete it?

AP models seem like they should be able to do better with much richer protein or peptide knowlege. GO features and protein
metrics seem very limited currently.

AP training data for expressionless models seems simpler. No expression data needed means we should have many more peptides to train on?
Do we actually do this?

Mapping indit pipeline steps to docker image names and then to repo names feels tedious.
I would love to be able to just go to definition in the same code base to find the implementation.

Spreading code into github repos makes it harder to link cursor to the right docs.

Set up a follow up meeting/check in second week? I spent a lot of time reading and testing and optimizing my computer and server setup.
Which I think is useful but I could also have dug into more tasks.

Fast is fun! How can we get faster?
No manual tests on PR. Auto test everything.

Part of why I want a closer to-mono repo approach is that I like using github for managing tasks.
And then the repo is a nice level of organization. When everything is spread out you need
jira to keep the state of what you're working on.

If we keep the indit manual in the repo we don't need to copy our doucentation out.
It will be tagged along with the code revision.
From the release guidelines
> Prepare documentation for release:
Create a copy of indit User Manual and rename it to contain release tag, e.g. INDIT v1.3.0 User Manual. Remove any sections unrelated to current release (e.g. WIP manuals for modules that cannot be run within indit).

We can also run doctest on the manual then!

I really want an automatic way to track server occupation. Confluence sheet is too much effort
for me to bother. I call "who" and if it is free I run my things.

Indit logs are filled with predictor progress bars. Would be nice to have these hidden
by default.

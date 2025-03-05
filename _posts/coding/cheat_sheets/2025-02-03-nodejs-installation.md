---
layout: post
title: 'Installation of multiple NodeJS versions'
date: 2024-02-03 18:30:00 +0200
categories: cheatsheet
author: 'Daria Graf'
---

# Node installation with brew

Firstly, we install the latest Node version on our MacBook by using the command `brew install node`.
After that, we install an older version of Node with `brew install node@20`.
After a successful installation, brew shows a message like:

```
If you need to have node@20 first in your PATH, run:
  echo 'export PATH="/opt/homebrew/opt/node@20/bin:$PATH"' >> ~/.zshrc
```

We can just execute this code and open the .zshrc file with `vim ~/.zshrc` and create command aliases for the different Node versions. The file will look something like this:

```bash
# Node settings
export PATH="/opt/homebrew/opt/node@23/bin:$PATH"

alias node20='export PATH="/opt/homebrew/opt/node@20/bin:$PATH"'
alias node23='export PATH="/opt/homebrew/opt/node@23/bin:$PATH"'
```

After that, we need to save the changes with `:wq` and restart the terminal.

With `node20` or `node23` we can switch between the versions. With `node -v` we can check the installed version.
# Fixing-Yarn-Global-Commands

I use Yarn to manage my node dependencies instead of npm, mostly because Rails chose it and it was much faster. To be fair, npm has improved since I first made my decision ([the release npm 7 supposedly had some really nice performance enhancements](https://github.blog/2021-02-02-npm-7-is-now-generally-available/) :tada:) but I'm pretty happy with yarn at this point and it is still what the Rails team recommends.

However, where I deviated on my love for yarn was when it came to globally installing packages. For some reason, global installs via yarn never seemed to produce an executable, whereas npm did. I hadn't been able to figure out the reason and I honestly didn't care, I just always globally installed packages via npm.

To illustrate what I mean, I will use [faressoft/terminalizer](https://github.com/faressoft/terminalizer) as an example.

```bash
yarn global add terminalizer
```

Weirdly, everything looks like it worked. Here is the output:

```bash
❯ yarn global add terminalizer

yarn global v1.22.10
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
[4/4] 🔨  Building fresh packages...
success Installed "terminalizer@0.7.2" with binaries:
      - terminalizer
✨  Done in 19.12s.
```

However, if I try to use the `terminalizer` command in my terminal, I get a command not found. In the past, this is where I would just run npm and move on:

```
npm install -g terminalizer
```

`¯\_(ツ)_/¯`

Today is different though because I just so happened to see a command in the Yarn documentation that would instantly reveal my issue.

>`yarn global bin` will output the location where Yarn will install symlinks to your installed executables.

Since I installed Yarn through [[homebrew]], I just assumed it would be `/usr/local/bin/yarn` without giving it another thought. It actually is pointing to an executable in the `asdf` folder for my current Node version.

>If you are unfamiliar with `asdf`, check out [How to install Ruby on Rails 6.1 with asdf on macOS Big Sur](https://andrewm.codes/blog/how-to-install-ruby-on-rails-6-1-with-asdf-on-macos-big-sur/).

```sh
❯ yarn global bin

/Users/andrew.mason/.asdf/installs/nodejs/14.16.0/.npm/bin
```

In order to run executables at this location, the file path has to be in my `PATH`. I know this because I spent way too much time debugging path issues earlier in my career due to my insistence on installing **all the things** when it came to styling my editor prompt. The outout of `echo $PATH` confirmed my suspicion: my environment doesn't know where it should be looking for all of the yarn executables I've tried to install.

Thankfully, the Yarn docs confirm that my `PATH` is the issue and also provide the solution:

>To use the installed packages, the install location has to be added to the PATH environment variable of your shell. For bash for example, you can add this line at the end of your .bashrc: `export PATH="$(yarn global bin):$PATH"`

I use zsh so I will add it to my zsh config instead of bash:

```bash
echo 'export PATH="$(yarn global bin):$PATH"` >> ~/.zshrc
```

Now if I restart my terminal and run:

```bash
yarn global add terminalizer
terminalizer record hello-world
```

It works! Our undefined error is gone and I am put into a recording session for terminalizer.

[Here's a link to my recording if you're curious!](https://terminalizer.com/view/30a427ab4731)

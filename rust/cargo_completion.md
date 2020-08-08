# bash auto-completion for Cargo

Cargo is the package manage tool for rust

rustup is the installer for rust and its tool chains

rustup do **download** completion scipts for cargo but do **not install** it when installing rust.

Since rustup would have to touch files outside of user home direcotry to install it.

So rustup leave this to us to config.

This command generate command to apply the auto-completion script

```bash
rustup completions <shell> cargo
```

for bash you can put it in .bash_profile like this

to set up automaticlly when login

```bash
rustup completions <shell> cargo >> ~/.bash_profile
```

# reference

original pull request at [here](https://github.com/rust-lang/rustup/pull/1646)
  

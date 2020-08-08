# bash auto-completion for Cargo

background:

1. **Cargo** is the package manage tool for rust
2. **rustup** is the installer for rust and its tool chains

rustup do **download** completion scipts for cargo but do **not install** it when installing rust.

Since that way, rustup would have to touch files outside of user home direcotry to install it.

So rustup leave this to us to config and give us some command to work with.

This command generate command to apply the auto-completion script

```bash
rustup completions <shell> cargo # <shell> can be *bash* or *zsh*
```

for bash you can put it in .bash_profile to set up automaticlly when login like this

```bash
rustup completions <shell> cargo >> ~/.bash_profile # <shell> can be *bash* or *zsh*
```

# reference

original pull request at [here](https://github.com/rust-lang/rustup/pull/1646)
  

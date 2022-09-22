### `dev-lang/rust` & `dev-lang/rust-bin` sucks!!! me want rustup!!

install rustup (duh)
  
`/etc/portage/bashrc`

```bash
# cargo uses this
export CARGO_HOME="/path/to/cargo/home"
  
# rustup uses this
export RUSTUP_HOME="/path/to/rustup/home"
  
# prefer rustup tools over system ones (if present)
export PATH="${CARGO_HOME}/bin:${PATH}"
```

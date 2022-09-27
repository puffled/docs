### `make.conf`

contains `KEY="value"` entries which ***globally*** apply

 - `ACCEPT_KEYWORDS=<keywords...>` is equivalent to `*/* <keywords...> `in `package.accept_keywords`
 - `CFLAGS`, `CXXFLAGS`, etc is equivalent to `*/* make.conf` in `package.env`
 - `INPUT_DEVICES="<flags...>"` is equivalent to `*/* input_devices: <flags...>` in `package.use`
 - `USE="<flags...>"` is equivalent to `*/* <flags...>` in `package.use`
 - `VIDEO_CARDS="<flags...>"` is equivalent to `*/* video_cards: <flags...>` in `package.use` 

### todo...

`bashrc`
`env`
`package.env`
`package.accept_keywords`
`package.unmask`
`package.mask`
`package.provided`

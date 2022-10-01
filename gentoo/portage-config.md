### `make.conf`


contains `KEY="value"` entries which ***globally*** (`*/*`) apply

equivalent to `*/* make.conf` in `package.env`, each `key="value(s)"` expands to `key: value(s)`

### `package.env`

regular categories

 - `CFLAGS`, `CXXFLAGS`, so on, is equivalent to `*/* env.conf` in `package.env`

special categories

 - `ACCEPT_KEYWORDS=<keywords...>` is equivalent to `<keywords...> `in `package.accept_keywords`
 - `INPUT_DEVICES="<flags...>"` is equivalent to `input_devices: <flags...>` in `package.use`
 - `USE="<flags...>"` is equivalent to `<flags...>` in `package.use`
 - `VIDEO_CARDS="<flags...>"` is equivalent to `video_cards: <flags...>` in `package.use` 

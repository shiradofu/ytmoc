## 🎵 YTMOC: YouTube Music On Console 🎵

### Requirements

- bash
- yq
- yt-dlp
- jackd
- mocp

### Basic Usage

Set environment variables below if you want:

```sh
export YTMOC_DIR="${YTMOC_DIR:-~/.ytmoc}"               # dir for playlists
export YTMOC_MP3_DIR="${YTMOC_MP3_DIR:-$YTMOC_DIR/mp3}" # dir for mp3 files
export YTMOC_DEFAULT_LIST="${YTMOC_DEFAULT_LIST:-main}"
export YTMOC_MOCOPT=${YTMOC_MOCOPT:-}
```

Create playlist YML file under `$YTMOC_DIR`.  
Note: only `.yml` is accepted. `.yaml` will be ignored.

Assumimg that we name the playlist file `example.yml`.

```yml
# $YTMOC_DIR/example.yml

# key is a youtube video id
# value is a title of the track (name as you like)

5xdKykxgfPA: Beethoven Piano Collection
2tduPwBo9uk: Bach Piano Collection
```

Run `sync` command.

```sh
ytmoc sync
```

Your `$YTMOC_DIR` and `$YTMOC_MP3_DIR` should look like:

```
$YTMOC_DIR
├── example
│   ├── 001.Beethoven Piano Collection.mp3 -> $YTMOC_MP3_DIR/5xdKykxgfPA.mp3
│   └── 002.Bach Piano Collection.mp3 -> $YTMOC_MP3_DIR/2tduPwBo9uk.mp3
└── example.yml

$YTMOC_MP3_DIR
└── mp3
    ├── 2tduPwBo9uk.mp3
    └── 5xdKykxgfPA.mp3

```

then, run `ytmoc open example` will open the 'example' playlist with mocp
frontend UI.

```
┌─────────────────────────────────┤$YTMOC_DIR/example├─────────────────────────────────┐
│../                                                                                   │
│001.Beethoven Piano Collection.mp3                                         [     |MP3]│
│002.Bach Piano Collection.mp3                                              [     |MP3]│
│                                                                                      │
│                                                                                      │
│                                                                                      │
│                                                                                      │
│                                                                                      │
├────┤                         ├──────────────────┤   soft mixer 100%  ├───┤>000:00:00├┤
│[] Welcome to Music On Console (version 2.5.2, revision 2930)!                        │
│00:00       [00:00]     kHz     kbps [STEREO] [NET] [SHUFFLE] [REPEAT] [NEXT]         │
└┤                                                                                    ├┘
```

### Command Usage

#### `ytmoc open`

```
ytmoc open [playlist name]
ytmoc o [playlist name]
ytmoc

Open the playlist with mocp frontend UI.
When playlist name (and subcommand) is omitted,
    1. If the last directory mocp opened is under $YTMOC_DIR, open it.
    2. If not, $YTMOC_DEFAULT_LIST will open.
```

#### ytmoc toggle

```
ytmoc toggle
ytmoc t

Toggle pause and unpause.
```

#### `quit`

```
ytmoc quit
ytmoc q

Shutdown the moc server.
```

#### ytmoc sync

```
ytmoc sync [playlist name]...

Sync $YTMOC_DIR and $YTMOC_MP3_DIR with passed playlists.
When no playlist given, it will target all playlists.
```

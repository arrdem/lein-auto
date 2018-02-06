# Lein-Auto
[![Clojars Project](https://img.shields.io/clojars/v/me.arrdem/lein-auto.svg)](https://clojars.org/me.arrdem/lein-auto)

A [Leiningen][] plugin that watches the project source directories, and
executes a task when it detects changes to files matching a set pattern.

[Leiningen]: https://github.com/technomancy/leiningen

## Installation

Add `lein-auto` as a plugin dependency to your project or profiles.

```clojure
:plugins [[me.arrdem/lein-auto "a.b.c"]]
```

## Usage

Add `auto` to the beginning of any command you want to be executed
when file changes are detected. For example:

```
lein auto test
```

This will run `lein test` every time it detects a change to a file.
You can stop it running with Ctrl-C.

By default only `.clj`, `.cljs`, `cljx` and `.cljc` files are watched. You can
change this by adding some extra configuration to your project file:

```clojure
:auto {:default {:file-pattern #"\.(clj|cljs|cljx|cljc|edn)$"}
```

The `:default` key will apply this option to all tasks, but you can
also apply options to a specific task:

```clojure
:auto {"test" {:file-pattern #"\.(clj|cljs|cljx|cljc|edn)$"}
```

There are currently four options available:

- `:paths` -
  a list of directory paths as strings, and keywords naming Leiningen paths. All paths are
  concatenated together and scanned for file changes according to the `:file-pattern`. When merging
  task-specific options with the `:default` options, `:paths` are concatenated (defaults to the
  `[:source-paths :java-source-paths :test-paths]`).

- `:file-pattern` -
  a regular expression that determine which files to watch (defaults
  to `#"\.(clj|cljs|cljx|cljc)$"`).

- `:wait-time` -
  the time to wait in milliseconds between polling the filesystem
  (defaults to 50)

- `:log-color` -
  the color of the Lein-Auto log messages (defaults to `:magenta`).
  The following colors are allowed: black gray white red green yellow
  blue magenta cyan bright-red bright-green bright-yellow bright-blue
  bright-magenta bright-cyan bright-white.

## License

Copyright © 2018 Reid "arrdem" McKenzie

Copyright © 2016 James Reeves

Distributed under the Eclipse Public License either version 1.0 or (at
your option) any later version.

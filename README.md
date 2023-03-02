[![Project Status: Abandoned – Initial development has started, but there has not yet been a stable, usable release; the project has been abandoned and the author(s) do not intend on continuing development.](https://www.repostatus.org/badges/latest/abandoned.svg)](https://www.repostatus.org/#abandoned)

# `minifySyntax` Experiments

## No JavaScript

First I want to get a baseline and then see what the difference is on a clean site.

`bridgetown new bt-esbuild-minifysyntax -t erb`

### Fresh 1.1.0

| Environment | JS Size | CSS Size | User Time | System Time |
| ----------- | ------- | -------- | --------- | ----------- |
| Development | 153B    | 4.25KB   | 0.49s     | 0.13s       |
| Production  | 113B    | 3.03KB   | 0.71s     | 0.20s       |

### Fresh `minifySyntax`

| Environment | JS Size | CSS Size | User Time | System Time |
| ----------- | ------- | -------- | --------- | ----------- |
| Development | 153B    | 3.86KB   | 0.48s     | 0.13s       |
| Production  | 113B    | 3.03KB   | 0.71s     | 0.18s       |

**So not much of a change for the JS size, though it did reduce the CSS size a bit.**

## Add JavaScript

Now let's run a bunch of configurators and see what happens when there is actual JS to be minified.

```sh
bridgetown configure turbo
bridgetown configure stimulus
bridgetown configure lit
bridgetown configure shoelace
```

### With JS

| Environment | JS Size  | CSS Size | User Time | System Time |
| ----------- | -------- | -------- | --------- | ----------- |
| Development | 285.52KB | 23.15KB  | 0.71s     | 0.16s       |
| Production  | 173.9KB  | 20.26KB  | 1.19s     | 0.85s       |

### With JS and `minifySyntax`

| Environment | JS Size | CSS Size | User Time | System Time |
| ----------- | ------- | -------- | --------- | ----------- |
| Development | 266KB   | 22.47KB  | 0.70s     | 0.16s       |
| Production  | 173.9KB | 20.36KB  | 1.16s     | 0.82s       |

Not a major difference in size but still a reduction in JS and CSS size. Over time though this adds up!

## TODO

- Try some more tweaks to the configurators.

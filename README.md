# libemoji &nbsp;[![Build Status](https://travis-ci.org/emoji-gen/libemoji.svg?branch=master)](https://travis-ci.org/emoji-gen/libemoji) [![wercker status](https://app.wercker.com/status/de905f978179bb9ca837a8b14d0cdf07/s/master "wercker status")](https://app.wercker.com/project/byKey/de905f978179bb9ca837a8b14d0cdf07) [![Osushi](https://img.shields.io/badge/donate-osushi-EA2F57.svg)](https://osushi.love/intent/post/9ad90add99954e62ac79251606c10eec)

:tada: Ultimate Emoji Generator library using [Skia](https://skia.org/)

<br>
<img src="emoji.png" width="128" height="128" alt="libemoji">

## System requirements

- CMake
- Python 2.7
- C11 Compiler
- C++14 Compiler

### Official supported platforms
- macOS Sierra
- Debian 9 Stretch

### macOS

```
$ brew install cmake
```

### Debian 9 Stretch

```
$ sudo apt-get update
$ sudo apt-get install git cmake g++ python libfontconfig1-dev \
    libx11-dev libxcomposite-dev libgl1-mesa-dev libglu1-mesa-dev freeglut3-dev -y
```

## How to build

```
$ git submodule update --init
$ cmake .
$ make
```

## Example

```c
#include "emoji.h"

int main(void) {
    EgGenerateParams params;
    memset(&params, 0, sizeof(params));
    params.fText = "絵文\n字。";
    params.fWidth = 256;
    params.fHeight = 256;

    EgGenerateResult result;
    if (emoji_generate(&params, &result) != EG_OK) {
        emoji_free(&result);
        return -1;
    }

    FILE *fp = fopen("./emoji.png", "w");
    fwrite(result.fData, result.fSize, 1, fp);
    fclose(fp);

    emoji_free(&result);
    return 0;
}
```

See also `example` directory.

## Development
### Run formatter

```
$ clang-format --version
clang-format version 7.0.0 (tags/google/stable/2018-04-24)

$ clang-format -i -style=file src/*.cpp src/*.h
```

## License
MIT &copy; [Emoji Generator](https://emoji-gen.ninja)

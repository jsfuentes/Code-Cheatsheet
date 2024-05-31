# ffmpeg

Industry standard video and audio encoder

## Setup

Is CLI, but has ports to most languages, even [WASM](https://github.com/ffmpegwasm/ffmpeg.wasm)

```bash
brew install ffmpeg
```

## Usage

To refer to input files in options, you must use their indices (0-based). E.g. the first input file is `0`, the second is `1`, etc. Similarly, streams within a file are referred to by their indices. E.g. `2:3` refers to the fourth stream in the third input file. Also see the Stream specifiers chapter.

As a general rule, options are applied to the next specified file.

## Example

- To set the video bitrate of the output file to 64 kbit/s:

  ```
  ffmpeg -i input.avi -b:v 64k -bufsize 64k output.avi
  ```

- To force the frame rate of the output file to 24 fps:

  ```
  ffmpeg -i input.avi -r 24 output.avi
  ```

- To force the frame rate of the input file (valid for raw formats only) to 1 fps and the frame rate of the output file to 24 fps:

  ```
  ffmpeg -r 1 -i input.m2v -r 24 output.avi
  ```
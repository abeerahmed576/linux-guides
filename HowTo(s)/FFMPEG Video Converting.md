### Converting:

```sh
ffmpeg -i <input> -c:v copy -c:a copy output.<format>

or,

ffmpeg -i <input> -c copy output.<format>
```

* `-c` stands for 'Codec'.
* `-c:a` means audio codec and `-c:v` means video codec.

### Resizing:

```sh
ffmpeg -i <input> -vf "scale= <w> : <h>" output.<format>
```

### Compressing:

```sh
ffmpeg -i <input> -c:v libx265 -crf 28 -c:a copy output.<format>
```

The higher the `-crf` value, the higher the compression resulting in lower size. Default value is 28 for `libx265`.

### Remove an audio or subtitle:

```sh
ffmpeg -i <input> -map 0 -map -0:a:2 -c copy output.<format>
```

* `-map 0` selects all streams from input video.(Video, audios, subtitles)
* `-map -0:a:2` then deselects('-' before '0' means deselecting) *audio* stream *3*.

> Note:
> * The stream index count starts from 0.
> * When specifying audio/video/subtitle stream like this:
> 
>     `-map 0 : a/v/s : 0/1/2/3`
> 
>   the 0th index is considered for the first audio/video/subtitle stream available. For example, if a video file has one video stream and two audio streams and we want to get rid of the first audio stream, we have to select/deselect the target stream using either of the syntaxes below:
> 
>   `-map -0:a:0` or `-map -0:1`
> 
>   For the second syntax, if we consider the list of all streams which consists of one video and two audio streams, then the video stream holds the index of 0 and the first audio stream or the target audio stream has the index of 1. Whereas specifying audio stream with 'a' in the first syntax changes the index of the target audio stream to 0.

### Adding subtitle to an mp4:

```sh
ffmpeg -i <video file> -i <subtitle file> -c:v copy -c:a copy -c:s mov_text output.mp4
```

### Extracting Subtitle from a video:

```sh
ffmpeg -i <input> -map 0:s:0 <output>.srt
```

`-map 0:s:0` selects the first subtitle stream of the input video.

### Batch Conversion:

1. Open Terminal and create a shell file:

    ```sh
    touch <filename>.sh
    ```

2. Make it executable:

    ```sh
    chmod +x <filename>.sh
    ```

3. Open the file with a text editor and paste the following code:

    ```sh
    #! /bin/<bash/zsh>
    for file in *.<extension>;
        do
        ffmpeg -i "$file" <Additional_Convertion_Options> "Converted/${file%.*}.<format>"
        done
    echo "Convertion Complete!"
    ```

    * The script will operate only on the files with the specified `<extension>`
    * *Additional_Convertion_Options* example:
      * `-c copy`
      * `-c:v libx265 -crf 28 -c:a copy`
      * `-vf "scale= <w> : <h>" `
      * `-map 0 -map -0:a:2 -c copy` etc.

    Save and close the text editor.

4. Copy/move the shell file to the target videos folder.

5. Create a folder: "Converted"

6. Open Terminal in the folder(not "Converted") and execute the shell file:

    ```sh
    ./<filename>.sh
    ```

    If the convertion is complete and successful, the new videos should be found in "Converted".

> Note: Names of the new videos will be the same as the originals after convertion.
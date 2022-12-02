# go-apriltag

## Description

Apriltags image recognition for Go.

Uses Cgo, but does not require any libraries or dependencies.

## Installation

This package can be installed with the go get command:

    go get github.com/sg3des/apriltag

**NOTE**: Make sure cgo works on your system.

Only tested on Linux, but should work (or need trivial modifications) to work on other platforms.

## Documentation

API documentation can be found here: http://godoc.org/github.com/twitchyliquid64/go-apriltag

Trivial example, finding apriltags in a PNG:

```go
detector := apriltag.New()
defer detector.Close()

f, err := os.Open("testtags.png")
if err != nil {
  log.Fatal(err)
}
defer f.Close()

img, err := png.Decode(f)
if err != nil {
  log.Fatal(err)
}

findings := detector.Find(apriltag.ImgToGrayscale(img)) // list of discovered tags

// If you want you can draw boxes around the tags
center := color.RGBA{R: 255, G: 0, B: 0, A: 255}
corner := color.RGBA{R: 0, G: 255, B: 0, A: 255}
apriltag.DrawFindings(img.(*image.RGBA), findings, center, corner)
```

[![Example output](https://github.com/twitchyliquid64/go-apriltag/raw/master/test_output.png)](https://github.com/twitchyliquid64/go-apriltag/raw/master/test_output.png)

## License

In this repository, those files are an amalgamation of code that was copied from Apriltag.
The license of that code is the same as the license of Apriltag.
Apriltag copyright notices remain intact as per license requirements.

For all non-Apriltag code, consider the license text as per the `LICENSE` file.

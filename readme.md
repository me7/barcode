// `sudo apt-get install libzbar-dev` to get zbar

package main

import (
	"fmt"
	"image/jpeg"
	"os"

	"gopkg.in/bieber/barcode.v0"
)

func main() {
	fin, _ := os.Open("card12.jpg")
	defer fin.Close()
	src, _ := jpeg.Decode(fin)

	img := barcode.NewImage(src)
	scanner := barcode.NewScanner().
		SetEnabledAll(true)

	symbols, _ := scanner.ScanImage(img)
	for _, s := range symbols {
		fmt.Println(s.Type.Name(), s.Data, s.Quality, s.Boundary)
	}
}

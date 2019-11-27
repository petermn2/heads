To build for X230 we need to have the following files in this folder:
* `me.bin` - ME binary that has been stripped and truncated with me_cleaner
* `gbe.bin` - Network card blob from the original firmware
* `descriptor.bin` - Flash layout file modified by me_cleaner

To get the binaries, start with a copy of the original 12M Lenovo firmware image.
If you do not have one already, you can read one out from the laptops SPI flash.
Make sure to boot Linux with the "iomem=relaxed" option on the commandline.

```
flashrom --programmer internal -r original.bin
```

Once you have the image, the provided extraction script will extract the files needed.

```
./extract.sh -f <romdump> -i <ifdtool>
```

The flash layout will be automatically adjusted and the ME image cleaned and truncated.

You can now compile the image with:

make BOARD=x230

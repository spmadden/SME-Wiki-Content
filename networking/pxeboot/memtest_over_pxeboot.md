## Memtest over PXEBoot

Follow the tutorial found in [PXE Boot Server](/networking/PXE Boot Server) to begin.

To allow Memtest to boot from the PXEBoot menu, follow the following steps.

-    Download memtest from <http://www.memtest.org/#downiso> . Make sure you download the Pre-Built Binary zip/gz file. This has the image we require.
-    Open a terminal and change directory to /tftpboot (or whichever directory you specified in the [PXE Boot Server](/networking/PXE Boot Server) tutorial.
-    Make a new directory called 'memtest'
-    cd into this directory.
-    The zip you downloaded will contain one file, a .bin file. Copy this bin file into the /tftpboot/memtest directory and rename it to 'memtest'. You MUST REMOVE the .bin extension or it WILL NOT BOOT!
-    Edit /tftpboot/pxelinux.cfg/default and add the following lines before 'MENU end'

```{=html}
<!-- -->
```
     LABEL Memtest
          MENU LABEL Memtest
          kernel memtest/memtest

Save the file, and start your testing method of choice. You should see an additional option entitled 'Memtest'. Select this and you should be booting into memtest. Congratulations!

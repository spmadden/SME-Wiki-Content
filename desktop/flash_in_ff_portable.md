## Flash in Firefox Portable

Installing flash in firefox is ridiculously easy. You will need two files, “flashplayer.xpt” and “NPSWF32.dll”. These can be found in one of two places:

-   If you already have flash installed on the system, you can simply copy the files into the /PortableApps/Firefox/App/Firefox/plugins directory. They can typically be found in “C:\\WINDOWS\\system32\\Macromed\\Flash” if the system came with the full version. Mine did not, so I had to go to plan B:

```{=html}
<!-- -->
```
-   The firefox .xpi (extention installer) is essentially a .zip archive that contains a javascript install file and the required files to install the plugin. Download the .xpi from <http://notepad.patheticcockroach.com/category/software/flash/#downloadSec> and open it using your favourite zip extractor. You will find the two files inside. Copy them to the plugins directory from above and restart firefox.

If all worked out well, you should now have flash functioning perfectly on your portable install (all without IT knowing about it).

## Custom Init Runlevels script

This is the file in \~/bin/init to replace the standard init script. It will only work if your home/bin directory is before /sbin in the path.

      #!/bin/bash
      if [ "$1" -eq 7 ] ; then
             sudo acpitool -s;
      else
             if [ "$1" -eq 8 ] ; then
                     sudo acpitool -S;
             else
                     sudo /sbin/init "$1";
             fi
      fi

It is setup such that the standard runlevels (0-6) are passed straight back to the /sbin/init script while level 7 is suspend-to-ram and runs

    acpitool -s

And runlevel 8 runs suspend-to-hdd

    acpitool -S

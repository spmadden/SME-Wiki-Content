## Windows hover follows mouse (X-Mouse)

Open regedit, go to HKEY_CURRENT_USER\\Control Panel\\Desktop

    Change UserPreferenceMask value to be 9F 3E 07 80 13

Also in HKEY_CURRENT_USER\\Control Panel\\Desktop

    Edit ActiveWndTrkTimeout, change 'Base' to Decimal and put in 150 as the 'Value Data'

this value is time in milliseconds that it takes for the focus to change. To avoid some issues with the taskbar I recommended using a value like 150 or so, but if you'd like to have a different delay before the window loses focus, set it to whatever you like.

You will have to log out to make this edit stick.

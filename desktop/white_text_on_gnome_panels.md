## White Text on Gnome Panels

You need to edit you \~/.gtkrc-2.0 file to include the following:

    style "modpanel"{
           fg[NORMAL] = "#FFFFFF"
    }
    widget "*PanelWidget*" style "modpanel"
    widget "*PanelApplet*" style "modpanel"
    widget "*switch-applet*" style "modpanel"
    widget "*SwitchApplet*" style "modpanel"

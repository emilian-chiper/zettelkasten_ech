### Meta
- - -
- 2024-09-14 12:21
- Tags: [[operating systems]] [[linux]] [[i3wm]]
- Status: #completed 

### Super key
- - -
- Super key is set to either Windows (Mod4) or Alt(Mod1) 
- To change the binding, modify the config file located in `./config/i3/config`.
- The first non-comment line should read `set $mod Mod4.`
- Reload i3 with `Win-Shift-R`.
- Forthwith, all shortcuts related to i3 will follow the convention `Win + Key`.

### Basics
- - -
- `Enter` open a new Terminal
- `J` focus Left.
- `K` focus Down.
- `L` focus Up.
- `;` focus Right.
- `a` focus Parent.
- `Space` toggle focus mode.

### Moving windows
- - -
- `Shift + J` move window Left.
- `Shit + K` move window Down.
- `Shit + L` move window Up.
- `Shit + ;` move window Down.

### Modifying windows
- - -
- `F` toggle fulscreen mode.
- `V` split window vertically.
- `H` splits window horizontally.
- `R` resize mode.

### Changing container layout
- - -
- `E` default.
- `S` stacking.
- `W` tabbed.

### Floating
- - -
- `Shift + Space` toggle floating.
- `Left click` drag floating.

### Using workspaces
- - -
- `0-9` switch to another workspace.
- `Shift + 0-9` move a window to another workspace.

### Opening / Closing applications
- - -
- `D` open application launcher (dmenu).
- `Shift + Q` kill a window.

### Restart / Exit
- - -
- `Shift + C` reload the configuration file.
- `Shift + R` restart i3 in place.
- `Shift + E` exit i3.

### END

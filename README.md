# ndrop

This nushell script emulates the main features of [tdrop](https://github.com/noctuid/tdrop) in [niri](https://github.com/YaLTeR/niri):

- if the specified program is not running: launch it and focus it.
- if the specified program is already running on another workspace: focus it.
<!-- - if the specified program is already on the current workspace: move it to workspace 'niri', thereby hiding it until called up again by ndrop. -->

<!-- > \[!NOTE] -->
<!-- > Niri doesn't implement scratchpads yet so nudrop is inferior to hdrop until they are added to niri. -->

#### Usage:

> nudrop [OPTIONS] [COMMAND]

#### Arguments:

> [COMMAND]  
> The usual command you would run to start the desired program

#### Options:

> -c, --class  
> Set classname of the program to be run. Use this if the classname is different from the name of the [COMMAND] and nudrop does not have a hardcoded replacement.
>
> -a, --app-id  
> Set app-id of the program to be run. Use this if the app-id is different from the name of the [COMMAND] and nudrop does not have a hardcoded replacement.
>
> -i, --insensitive  
> Case insensitive partial matching of class names. Can work as a stopgap if a running program is not recognized and a new instance is launched instead. Note: incorrect matches may occur, adding a special handling of the program to nudrop (hardcoded or via `-c, --class`) is preferable.
>
> -o, --online  
> Delay initial launch for up to 20 seconds until internet connectivity is established.

#### Multiple instances:

Multiple instances of the same program can be run concurrently, if different class names are assigned to each instance. Presently, there is support for the following flags in the [COMMAND] string:

> `-a` | `--app-id` ([foot](https://codeberg.org/dnkl/foot/) terminal emulator)  
> `--class` (all other programs)

#### Example bindings in niri config:

```kdl
binds {
    Mod+e { spawn "nudrop" "kitty" "--class" "kitty_1"; }
    Mod+Alt+e { spawn "nudrop" "kitty" "--class" "kitty_2"; }
    Mod+a { spawn "nudrop" "kitty" "--class" "kitty_hx" "hx"; }
    Mod+Alt+a { spawn "nudrop" "kitty" "--class" "kitty_code"; }
}
```

> \[!NOTE] 
> Defining a class name is only necessary when running multiple instances of the same program at the same time.

## Troubleshooting

<!-- ### Programs are not moved away from the present workspace -->

<!-- Please see the example bindings. There has to be a workspace named `nudrop` for nudrop to work and `nudrop` may not be your present workspace. -->

<!-- Niri doesn't implement scratchpads yet so the behaviour of `nudrop` is inferior to `hdrop`. -->

<!-- ### Further instances of programs are started instead of hiding/unhiding a running instance -->

<!-- If nudrop can't match an already running program and starts a new instance instead, then its class name is most likely different from its command name. For example, the class name of `telegram-desktop` is `org.telegram.desktop` and the class name of `logseq` is `Logseq`. -->

<!-- Run `nudrop -v [COMMAND]` _in the terminal_ to see maximum output for troubleshooting and find out the actual class name. Then use `nudrop -c CLASSNAME` to make it work. `nudrop -i [COMMAND]` might be sufficient, as long as a case insensitive (partial) match is sufficient. -->

<!-- Please report instances of programs with differing class names, so that they can be added to `nudrop`. -->

## Installation

### Repositories

[![Packaging status](https://repology.org/badge/vertical-allrepos/nudrop.svg)](https://repology.org/project/nudrop/versions)

## See also

[ndrop](https://github.com/schweber/ndrop) is the bash version of this script for [niri](https://github.com/YaLTeR/niri).

[hdrop](https://github.com/schweber/hdrop) is the bash version of this script for [hyprland](https://github.com/hyprwm/hyprland).

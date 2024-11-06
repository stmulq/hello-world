# BrightScript Debugger

This page serves as a guide for accessing the **BrightScript Debugger** of BrightSign players. The BrightScript Debugger can be accessed via a physical serial connection or over the network via SSH or Telnet. For the physical serial connection, certain cables are recommended as described [here](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/1988100153/BrightSign+Shell+and+BrightScript+Debugger#Serial-Cable-Hardware).

## What is the BrightScript Debugger?

> [!INFO]
> The BrightScript Debugger is sometimes referred to as the BrightScript Debug Console. However, in an effort to maintain consistency and to avoid potential confusion, the term BrightScript Debugger, or more simply, Debugger, is predominantly used.

The BrightScript Debugger is a CLI which enables interaction with the BrightScript Interpreter. It is denoted by the prompt `BrightScript Debugger>` and is a powerful tool for troubleshooting and debugging issues with BrightScript scripts or interacting with BrightScript objects. It is similar to the JavaScript console in web browsers as well as other popular debuggers (e.g., GDB). Developers can set stop statements (a breakpoint), step through a BrightScript script, and gain access to the current scope or initialized variables.

If the BrightScript Debugger has not been enabled, runtime errors will often cause the player to reboot. When the BrightScript Debugger is enabled, runtime errors will cause the BrightSignOS to stop on the line of the runtime error, allowing a step-through of the script.

> [!WARNING]
> Since enabling the BrightScript Debugger will cause the player to hang when runtime errors are encountered, the BrightScript Debugger should only be used in development environments or debugging situations; it should be disabled for production deployments.

## BrightSign Console

The BrightSign Console (or more simply, Console) enables access to the BrightSign Shell, BrightScript Debugger, and logs over the 3.5mm serial port. More information about the BrightSign Console and how to enable it can be found [here](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/1988100153/BrightSign+Shell+and+BrightScript+Debugger#Enabling-the-BrightSign-Console).

## Enabling the Debugger

The Debugger is enabled by writing a registry key to the player’s registry. This can be done in several ways as described below.

### From the BrightSign Shell

Type the following from the [BrightSign Shell](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/1988100153/BrightSign+Shell):

```
script debug on
```

### DWS Registry Tab

From the DWS Registry tab in BrightAuthor:connected, submit the following command:  
`registry write brightscript debug 1`

### Inclusion with Autorun

The following lines can be included as part of an autorun.brs file:

```
reg = CreateObject("roRegistrySection", "brightscript")
reg.write("debug","1")
```

### Accessing the Debugger

When enabled, the Debugger is denoted by the prompt `BrightScript Debugger>` and is accessible through a serial cable, Telnet, or SSH.

Navigate to the Debugger through one of the methods described below.

If you have not enabled the Debugger, any interruption to the BrightScript Interpreter execution will not give access to the Debugger. Instead, the player will reboot to attempt a clean execution.

#### During Runtime

Press CTRL-C on your keyboard while the player is powered on.

#### Runtime Stop Statement

If the Debugger has been enabled, the player will enter the Debugger if a runtime error occurs or a STOP statement is encountered while a script is running.

#### Access at Bootup

1.  Power off the player.
    
2.  Power on the player and wait 5-15 seconds.
    
3.  Press and hold the SVC button on the player for 15-30 seconds until the `BrightSign>` prompt appears in the serial/Telnet/SSH terminal app. The `BrightSign>` prompt indicates that you are in the BrightSign Shell. You can now release the SVC button.
    

If you are using Telnet or SSH, you will need to restart the Telnet or SSH instance.

#### Additional Methods

*   Press CTRL-C in your terminal app that is connected to the player.
    
*   Remove the microSD card and press either the SVC button on the player or CTRL-C on your computer.
    
*   If the serial console has been enabled (either temporarily or persistently), `Starting BrightSign Application...` will appear after the player reboots (note that this can take up to 30 seconds). Press and hold the SVC button until the `BrightSign>` prompt displays.
    
*   If you have removable storage such as a microSD card, eject it. Reboot the player and press the SVC button. If you are accessing the player through Telnet, you will have to restart the Telnet connection after the player reboots using the telnet {{your player IP address}} 23 command.
    
*   Place an autorun.brs file containing only the word “end” (without the quotes) on the storage device. The script will execute and when it ends as instructed you’ll be left at the `BrightSign>` prompt.
    

> [!INFO]
> Note: BrightSignOS does not register the SVC button event if there is no autorun.brs on the storage device.

This will break out of the application running at the moment and redirect to the BrightSign prompt.

## Debugger Commands

The following Shell commands are currently available in the Debugger:

| Command | Description |
| --- | --- |
| `bt` | Print a backtrace of call-function context frames. |
| `classes` | List all public classes. |
| `cont` or `c` | Continue script execution. |
| `counts` | List count of BrightScript Component instances. |
| `da` | Show disassembly and bytecode for this function. |
| `down` or `d` | Move one position down the function context chain. |
| `exit` | Exit the debug shell. |
| `gc` | Run the garbage collector and show collection statistics. |
| `hash` | Print the internal hash-table histograms. |
| `last` | Show the last line that executed. |
| `methods <class>` | List methods provided by specified class. |
| `methods <class>.<interface>` | List methods provided by the specified interface or class. |
| `list` | List the current source of the current function. |
| `ld` | Show line data (source records) |
| `next` | Show the next line to execute. |
| `bsc` | List all allocated BrightScript Component instances. |
| `stats` | Show statistics. |
| `step` or `s` | Step one program statement. |
| `t` | Step one statement and show each executed opcode. |
| `up` or `u` | Move one function up the context chain. |
| `var` | Display local variables and their types/values. |
| `print` or `p` or `?` | Print variable value or expression.\* |

\*BrightScript `print` messages are routed to the BrightSignOS which is accessible via the primary serial port or Telnet/SSH.

## Switch Between the Shell and the Debugger

From the `BrightSign>` prompt, type `script` to navigate to the Debugger:

```
script
```

From the `BrightScript Debugger>` prompt, type `exit` to navigate to the BrightSign Shell:

```
exit
```

## Telnet and SSH

The Debugger can be accessed with Telnet or SSH. More info can be found [here](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/1988100153/BrightSign+Shell+and+BrightScript+Debugger#Telnet).

## Debugging BrightScript Code

This section will cover how to debug BrightScript code on a BrightSign player assuming the Debugger has been enabled and is accessible.

See [BrightScript](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370672718/BrightScript) for information regarding BrightSign’s documentation for BrightScript. Our interpreter forked from Roku’s BrightScript language many years ago and have since diverged.

### How to Debug BrightScript

To begin stepping through or debugging BrightScript code, add a `stop` statement to the line of code you want to start debugging from.

A `stop` statement is a breakpoint in the BrightScript code. When the BrightSign player encounters a `stop` statement, it will break and enter the BrightScript Debugger when the debugger is enabled.

The BrightScript Debugger is similar to many other debuggers, e.g., gdb. It allows you to step through the code, inspect variables, and evaluate expressions.

Type `help` in the Debugger to see a list of available commands. Type `vars` to see the variables and their values.

### Debugging JavaScript or Node.js

To enable the Chrome Devtools and add BrightSign’s remote inspector, see [Debugging Webpages](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370672286/HTML+Best+Practices#Debugging-Webpages).

Navigate to `chrome://inspect` adding the IP Address of your player on the same network as your Computer.

## Troubleshooting

If you’re encountering difficulties connecting your terminal application to the BrightSign player, see the troubleshooting steps outlined [here](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/1988100153/BrightSign+Shell#Troubleshooting).

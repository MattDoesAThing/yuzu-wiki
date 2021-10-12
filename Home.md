yuzu emulator
=============
yuzu is an experimental open-source emulator for the Nintendo Switch from the creators of [Citra](https://citra-emu.org/). It is written in C++ with portability in mind, with builds actively maintained for Windows and Linux. yuzu is licensed under the GPLv2 (or any later version). Refer to the license.txt file included.

Check out our [website](https://yuzu-emu.org/)!

For development discussion, please join us on [Discord](https://discord.gg/u77vRWY).

## Development

Most of the development happens on GitHub. It's also where [our central repository](https://github.com/yuzu-emu/yuzu) is hosted.

If you want to contribute please take a look at the [Contributor's Guide](https://github.com/yuzu-emu/yuzu/blob/master/CONTRIBUTING.md) and [Developer Information](https://github.com/yuzu-emu/yuzu/wiki/Developer-Information). You should as well contact any of the developers on Discord in order to know about the current state of the emulator.

## Usage
You may download a precompiled binary from [our website](https://yuzu-emu.org/downloads/), or you can build it yourself from the source code.

* __Windows__: [Windows Build](https://github.com/yuzu-emu/yuzu/wiki/Building-For-Windows)
* __Linux__: [Linux Build](https://github.com/yuzu-emu/yuzu/wiki/Building-For-Linux)

**Note: macOS is no longer supported due to Apple deprecating OpenGL and their current version not supporting the OpenGL extensions we require.** ([source](https://www.anandtech.com/show/12894/apple-deprecates-opengl-across-all-oses))

## Log Filters

Yuzu supports configurable filtering of log message per-class. This is especially useful if you’re debugging a subsystem and want very detailed messages from it or if you want to silence some annoyingly spammy errors (e.g. unimplemented GPU features.)

Messages are filtered in each class according to their severity, the filter will block all messages in the class that are below the configured severity.

The severity levels are:
  - Trace: Extremely detailed and repetitive (many times per frame) debugging information that is likely to pollute logs.
  - Debug: Less detailed debugging information.
  - Info: Status information from important points during execution.
  - Warning: Minor or potential problems found during execution of a task.
  - Error: Major problems found during execution of a task that prevent it from being completed.
  - Critical: Major problems during execution that threathen the stability of the entire application. (This severity cannot be filtered out.)

**Note: Trace is permanently filtered out in non-Debug builds for performance reasons.**

Class names can be discovered from the log messages themselves. For example, this message is in the class Service:

``[  10.285042] Service  core/hle/service/service.h:Service::Interface::SyncRequest:84: unknown/unimplemented function '0x01020000': port=APT:U``

[A complete list can be found in the source](https://github.com/yuzu-emu/yuzu/blob/a39760b9471283c2d856075b382444e961d78390/src/common/logging/filter.cpp#L65)

To configure the log filter, you need to change the configuration in:

Emulation -> Configure... -> General -> Debug tab. Change the Global Log Filter setting.

The filter string consists of a space-separated list of filter rules, each of the format:

  `Class.Subclass:Severity` -- a log class name, with subclasses separated using periods.  
  `*:Severity` -- wildcards are allowed and can be used to apply a rule to all classes. 

A severity level name which will be set as the minimum logging level of the matched classes. Rules are applied left to right, with later rules overriding previous ones in the sequence.

A few examples of filter rules: 
  - *:Info – Resets the level of all classes to Info.
  - Service:Info – Sets the level of Service to Info (without affecting its subclasses).
  - Service.FS:Trace – Sets the level of the Service.FS class to Trace.

## Support
We happily accept monetary donations or donated games and hardware. Please see our [donations page](https://yuzu-emu.org/donate/) for more information on how you can contribute to yuzu. Any donations received will go towards things like:
* Switch consoles to explore and reverse-engineer the hardware
* Switch games for testing, reverse-engineering, and implementing new features
* Web hosting and infrastructure setup
* Software licenses (e.g. Visual Studio, IDA Pro, etc.)
* Additional hardware (e.g. GPUs as-needed to improve rendering support, other peripherals to add support for, etc.)

We also more than gladly accept used Switch consoles, preferably ones with firmware 3.0.0 or lower! If you would like to give yours away, don't hesitate to join our [Discord](https://discord.gg/u77vRWY) and talk to bunnei. You may also contact: [donations@yuzu-emu.org](mailto:donations@yuzu-emu.org).

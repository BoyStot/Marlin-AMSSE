# Anycubic Mega-SSE Marlin 1.1.9 by Stot

This is a custom version of the [Marlin Firmware](https://github.com/MarlinFirmware/Marlin) for the Anycubic Mega-S, based on [ davidramiro's repo](https://github.com/davidramiro/Marlin-Ai3M).

## Why use this?

Other than the great updates added by Davids repo this fork has support for the Stot Switching Extruder (SSE), a single stepper extruder capable of automatically switching between 4 filaments by utilizing one of the servo signals. As long as you dont have a bltouch for example this means without any hardware changes.  If you do you will need to solder on a servo header to one of the free servo signal pads.

To support this a new '> SSE Menu' has been added to select active filaments and load/unload them on the Anycubic TFT.  This allows you to use standard one colour sliced files and simply select from one of the 4 loaded filaments.

I also made the existing 'Special' menu easier to read and in a more natural order.

## Custom G-Codes

I have added 2 custom gcode commands to use for loading and unloading filaments.  Without any extra parameters these will use the Configuration.h settings COMBINER_LENGTH, COMBINER_TO_COOLING_BOWDEN_LENGTH and COOLING_TUBE_LENGTH all of which can be overwritten by entering them on the gcode.

### M751 Load Filament

This will load the filament from the parked position to the hot end.

Optional parameters are

 #### C\<distance\>
 Cooling tube length in mm. If omitted COOLING_TUBE_LENGTH is used.
 #### Y\<distance\> 
 Length of the Y filament combiner in mm from output to input furthest from output. If omitted COMBINER_LENGTH is used.
 #### B\<distance\> 
 Bowden tube Length in mm from the top of the cooling tube to the output of the filament combiner. If omitted COMBINER_TO_COOLING_BOWDEN_LENGTH is used. 

### M752 Unload Filament

This will perform a series of extruder operations to minimise stringing then extract the filament back to the park position.

Optional parameters are

 #### C\<distance\>
 Cooling tube length in mm. If omitted COOLING_TUBE_LENGTH is used.
 #### Y\<distance\> 
 Length of the Y filament combiner in mm from output to input furthest from output. If omitted COMBINER_LENGTH is used.
 #### B\<distance\> 
 Bowden tube Length in mm from the top of the cooling tube to the output of the filament combiner. If omitted COMBINER_TO_COOLING_BOWDEN_LENGTH is used. 
 
## How to flash this?

- Download and install [Arduino IDE](https://www.arduino.cc/en/main/software)
- Clone or download this repo
- Browse into the Marlin folder and run `Marlin.ino`
- In the IDE, under `Tools -> Board` select `Genuino Mega 2560` and `ATmega2560`
- Open Marlin.ino in the Marlin directory of this repo
- [Customize if needed based on davidramiros repo](https://github.com/davidramiro/Marlin-AI3M/wiki/Customization-&-Compiling) (e.g. motor directions and type at line `559` to `566` and line `857` to `865` in `Configuration.h`)
- Under `Sketch`, select `Export compiled binary`
- Look for the .hex file in the Marlin directory (only use the `Marlin.ino.hex`, not the `Marlin.ino.with_bootloader.hex`!)

### After obtaining the hex file:

- Flash the hex with Cura, OctoPrint or similar

## Updating
### Anycubic i3 Mega

This repo can be used on the AnyCubic i3 Mega if the configuration.h file is editied as per [davidramiro's repo](https://github.com/davidramiro/Marlin-Ai3M).

### Back up & restore your settings

Some updates require the storage to be cleared (`M502`), if mentioned in the update log. In those cases, before updating, send `M503` and make a backup of all the lines starting with:

```
M92
G29
M301
M304
```

After flashing the new version, issue a `M502` and `M500`. After that, enter every line you saved before and finish by saving with `M500`.

## Something went wrong?
No worries. You can easily go back to the default firmware and restore the default settings.
- Flash the hex file from the [manufacturer's website](http://www.anycubic3d.com/support/show/594016.html)
- After flashing, send `M502` and `M500`. Now your machine is exactly as it came out of the box.

## About Marlin

<img align="right" src="../../raw/1.1.x/buildroot/share/pixmaps/logo/marlin-250.png" />

Marlin is an optimized firmware for [RepRap 3D printers](http://reprap.org/) based on the [Arduino](https://www.arduino.cc/) platform. First created in 2011 for RepRap and Ultimaker printers, today Marlin drives a majority of the world's most popular 3D printers. Marlin delivers outstanding print quality with unprecedented control over the process.

[![Coverity Scan Build Status](https://scan.coverity.com/projects/2224/badge.svg)](https://scan.coverity.com/projects/2224)
[![Travis Build Status](https://travis-ci.org/MarlinFirmware/Marlin.svg)](https://travis-ci.org/MarlinFirmware/Marlin)
[![Flattr Us!](http://api.flattr.com/button/flattr-badge-large.png)](https://flattr.com/submit/auto?user_id=ErikZalm&url=https://github.com/MarlinFirmware/Marlin&title=Marlin&language=&tags=github&category=software)


### Contributing to Marlin

If you have coding or writing skills you're encouraged to contribute to Marlin. You may also contribute suggestions, feature requests, and bug reports through the Marlin Issue Queue.

Before contributing, please read our [Contributing Guidelines](https://github.com/MarlinFirmware/Marlin/blob/1.1.x/.github/contributing.md) and [Code of Conduct](https://github.com/MarlinFirmware/Marlin/blob/1.1.x/.github/code_of_conduct.md).

### Marlin Resources

- [Marlin Home Page](http://marlinfw.org/) - The latest Marlin documentation.
- [Marlin Releases](https://github.com/MarlinFirmware/Marlin/releases) - All Marlin releases with release notes.
- [RepRap.org Wiki Page](http://reprap.org/wiki/Marlin) - An overview of Marlin and its role in RepRap.
- [Marlin Firmware Forum](http://forums.reprap.org/list.php?415) - Get help with configuration and troubleshooting.
- [Marlin Firmware Facebook group](https://www.facebook.com/groups/1049718498464482) - Help from the community. (Maintained by [@thinkyhead](https://github.com/thinkyhead).)
- [@MarlinFirmware](https://twitter.com/MarlinFirmware) on Twitter - Follow for news, release alerts, and tips. (Maintained by [@thinkyhead](https://github.com/thinkyhead).)

### Credits

Marlin's administrators are:
 - Scott Lahteine [[@thinkyhead](https://github.com/thinkyhead)]
 - Roxanne Neufeld [[@Roxy-3D](https://github.com/Roxy-3D)]
 - Bob Kuhn [[@Bob-the-Kuhn](https://github.com/Bob-the-Kuhn)]
 - Erik van der Zalm [[@ErikZalm](https://github.com/ErikZalm)]

Notable contributors include:
 - Alexey Shvetsov [[@alexxy](https://github.com/alexxy)]
 - Andreas Hardtung [[@AnHardt](https://github.com/AnHardt)]
 - Ben Lye [[@benlye](https://github.com/benlye)]
 - Bernhard Kubicek [[@bkubicek](https://github.com/bkubicek)]
 - Bob Cousins [[@bobc](https://github.com/bobc)]
 - Petr Zahradnik [[@clexpert](https://github.com/clexpert)]
 - Jochen Groppe [[@CONSULitAS](https://github.com/CONSULitAS)]
 - David Braam [[@daid](https://github.com/daid)]
 - Eduardo José Tagle [[@ejtagle](https://github.com/ejtagle)]
 - Ernesto Martinez [[@emartinez167](https://github.com/emartinez167)]
 - Edward Patel [[@epatel](https://github.com/epatel)]
 - F. Malpartida [[@fmalpartida](https://github.com/fmalpartida)]
 - João Brazio [[@jbrazio](https://github.com/jbrazio)]
 - Kai [[@Kaibob2](https://github.com/Kaibob2)]
 - Luc Van Daele [[@LVD-AC](https://github.com/LVD-AC)]
 - Alberto Cotronei [[@MagoKimbra](https://github.com/MagoKimbra)]
 - Marcio Teixeira [[@marcio-ao](https://github.com/marcio-ao)]
 - Chris Palmer [[@nophead](https://github.com/nophead)]
 - Chris Pepper [[@p3p](https://github.com/p3p)]
 - Steeve Spaggi [[@studiodyne](https://github.com/studiodyne)]
 - Thomas Moore [[@tcm0116](https://github.com/tcm0116)]
 - Teemu Mäntykallio [[@teemuatlut](https://github.com/teemuatlut)]
 - Nico Tonnhofer [[@Wurstnase](https://github.com/Wurstnase)]
 - [[@android444](https://github.com/android444)]
 - [[@bgort](https://github.com/bgort)]
 - [[@GMagician](https://github.com/GMagician)]
 - [[@Grogyan](https://github.com/Grogyan)]
 - [[@maverikou](https://github.com/maverikou)]
 - [[@oysteinkrog](https://github.com/oysteinkrog)]
 - [[@paclema](https://github.com/paclema)]
 - [[@paulusjacobus](https://github.com/paulusjacobus)]
 - [[@psavva](https://github.com/psavva)]
 - [[@Tannoo](https://github.com/Tannoo)]
 - [[@teemuatlut](https://github.com/teemuatlut)]
 - ...and many others

## License

Marlin is published under the [GPLv3 license](https://github.com/MarlinFirmware/Marlin/blob/1.0.x/COPYING.md) because we believe in open development. The GPL comes with both rights and obligations. Whether you use Marlin firmware as the driver for your open or closed-source product, you must keep Marlin open, and you must provide your compatible Marlin source code to end users upon request. The most straightforward way to comply with the Marlin license is to make a fork of Marlin on Github, perform your modifications, and direct users to your modified fork.

## Disclaimer

```
/*
* Flashing a custom firmware happens at your own risk.
*
* THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS
* AND CONTRIBUTORS “AS IS” AND ANY EXPRESS OR IMPLIED
* WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
* WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A
* PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL
* THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR
* ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
* CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
* PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS
* OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION)
* HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER
* IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE
* OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
* SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
*/
```

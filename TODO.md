### TODO

Items listed here should be changed one at a time, and the line marked done, this
file and the changed files committed together. After a session of N changes the
PDF should be updated and pushed. The PDF should not be updated with each and
every change as there is no benefit and a binary repository size drawback.

 - Fred and Dan to discuss/review reverse polarity behaviour of the current schematic and connection topology. Next skype.
 - Correct lables on RPM1a inputs, which are backward. Spotted by Dan, good work, sir! :-)
 - DONE, Fix the load jumper and CEL circuit by adding a resistor between it and the CPU like this: http://stuff.fredcooke.com/LoadAndCELCorrectJumperTopology.png
 - Deferrable: Spend some time to properly tune the ADC filter capacitor values - Fred and Dan and others
 - Deferrable: Experiment with layouts to validate pin arrangement selection for header, and decide if Knock/RS232/Dual-reg setup is possible to fit for 0.1

### Once branched for layout-0.1-alpha (RC2)

Fred and Dan to do this together like last time in a session.

 - Remove the SD card sheet, 3.3V power supply, and X the pins on the CPU sheet, etc.
 - Correct annotation sheet order before annotating
 - Annotate the schematics with designators
 - Update all notes with designators to match new numbering (remove ?)
 - Generate new PDF for review
 - Update the TODO to reflect current goals on branch and new single hash of all files post annotation
 - Tag repository as Schem-0.1-alpha-RC2
 - Import BOM from RC1, adjust references to suit new schematic annotations, commit BOM (do we need PDF of this? I think not.)

### Still To Add/Do

Known issues which don't have a solution 100% nailed down yet.

Required for a final board revision to be top quality:

 1. Confirm pin selection for simple bit banged IO like tacho etc: Fred + others: http://forum.diyefi.org/viewtopic.php?f=8&t=1676
 2. Finalise selection of wakeup pin - Fred http://forum.diyefi.org/viewtopic.php?f=8&t=1266
 3. Power supply page - requires design, discuss http://forum.diyefi.org/viewtopic.php?f=58&t=1478

Easy stuff to do last:

 1. Tune the ADC input filters - Fred + consultation
 2. Annotate all components in the schematics
 3. Add to and correct the NOTES.md file

Stuff that's still in progress, but good enough already:

 1. DONE! (enough) Develop new improved SM - Fred http://forum.diyefi.org/viewtopic.php?f=8&t=1232

And perhaps more.

### SD card sheet changes

Discuss all SD card sheet changes before doing anything, skype, IRC and forum: http://forum.diyefi.org/viewtopic.php?f=58&t=1479

 - Improve layout of SD card sheet - Preston wants to do this
 - Move 3.3V regulator to 12V input such that sharp current changes don't affect our analogue stuff
 - Use regulator with enable input and parallel with analogue enable on 5V setup
 - Reduce post reg capacitor to 47uF tantalum
 - Change 1.0uF to 0.1uF ceramics on both sides of 3.3V reg
 - Move all 3.3V power supply caps to power supply sheet

All pages that are changed must be rechecked and enter another cycle of fix and
then check or be confirmed good and then locked down.

### Connector pin ordering

At least four concerns guide the selection of pin to function mappings. By far
the most important of these is noise considerations. For this reason the layout
should maintain the following block ordering:

 1. RPM Inputs (hyper sensitive)
 2. Analogue Inputs (and 5V/Ground for them) (very sensitive)
 3. Digital Inputs (very sensitive)
 4. Ignition Outputs, low current (not sensitive, not noisy)
 5. Fuel pump relay drive (not sensitive, potential to be noisy)
 6. Spare LSD Outputs (not sensitive, usually noisy, when used)
 7. ISCV Outputs (not sensitive, usually noisy, when used)
 8. Injector Outputs (not sensitive, always noisy, when used)
 9. Power and Grouds (not sensitive, grounds always noisy)

The other three concerns are these:

 1. Intuitive User Order
 2. Fine grain routing
 3. Schematic Aesthetics

1 and 2 are of similar importance, and 3 should take a back seat to the others,
while still being kept in mind for ease of comprehension. As such the designers
are free to reorder pins of this sheet during the layout process to facilitate a
better, lower noise, simpler, cleaner, more compact, more comprehensible for the
user layout. Aside from the block ordering, the page should be kept with all
inputs and ignition drivers on the left and all high current and high noise
connections on the right. This sheet reordering does not need to follow the
usual process of agree, TODO, action, and can be done at the designers will.
Although this breaks with the process, it provides significant benefits in both
speed of development and quality of development. Thus it is worth doing this way.

The spare pins header sheet is subject to the same freedoms for layout reasons.

Pin ordering follows this diagram, except the grounds have been rearranged http://stuff.fredcooke.com/RavagePinOutAttempt2.png

### Pre-Layout Lock Down

As each sheet becomes a perfect representation of what we want to see in RavAGE
it will get locked. That is to say, no further changes to that sheet's source
.SchDoc file will be allowed without agreement between all key players.

Locked sheets will be listed here as they are finalised:

 - Spare IO Header @ NO pending possible rearrangement
 - Core analogue inputs @ NO pending value selection
 - Extra analogue inputs @ NO pending value selection
 - USE 0.1 TO TEST: @ b36bb33d Digital and wake up inputs @ NO pending wake up testing
 - Connector pin out @ ecdaed700b58eaaf16ad0ddf4c48198efca5d85a
 - CPU and buses, etc @ 14eae84ad1f2c094e9d5b6bee46bd3429c172d74
 - USB communications @ e70d478d8635a083402ecfb5f5f076b4fc3c8185
 - RS232 communications @ 247e1f109145382aaa98ed5c90c7676b9f4068cd
 - RPM conditioned inputs @ c40a0885fad16cf92aaf213e950141aef8fa67e1
 - Knock sensor inputs @ 1450ad98dc2e1c864d0d5789b42a16420bbd773e
 - Igniter output drivers @ fc591f538e7f880f76d490ce6b23da58f4e1e481
 - Injector output drivers @ 7ad534dc22ba7a4618d42d22ae2bb547ddda230f
 - GP low side drivers @ 0e0ec7b1f4f0095ec0caf7929a33b819e120481e
 - 3-wire ISCV drivers @ 7ad534dc22ba7a4618d42d22ae2bb547ddda230f
 - OK FOR 0.1 @ e50be379d But not final. Power supplies @ NO pending discussion and design
 - UNUSED FOR 0.1: SD card slot @ NO pending multiple changes

### PDF Sheet Ordering

All sheets except for the CPU/navigation sheet will be A4 size. The CPU sheet
needs to be larger to fit the minimum required items on it. The sheet ordering
should be kept consistent on every commit. Preferred ordering is as follows.

 1.  CPU, decoupling, etc
 2.  Power supplies
 3.  USB communications
 4.  RS232 communications
 5.  RPM conditioned inputs
 6.  Core analogue inputs
 7.  Extra analogue inputs
 8.  Digital and wake up inputs
 9.  Knock sensor inputs
 10. Igniter output drivers
 11. Injector output drivers
 12. GP low side drivers
 13. 3-wire ISCV drivers
 14. SD card slot
 15. Spare IO Header
 16. Connector pin out

### Space Constraints

Due to the target board size and the level of things included so far, some
items could get cut when layout starts and we start getting a feel for
realistic limitations. The current plan is a 2-layer board with all features
that are currently in the schematics. I will list the possible changes below.

 - Change from 2-layer to 4-layer. Benefits more compact, better noise resistance. Drawbacks, more expensive, mildly less hackable.
 - Remove SD card slot and 3.3V power supply components
 - Remove RS232 interface for LC-1 and other products
 - Remove knock sensing interface circuit
 - Drop always-on support and RTC in favour of a simpler key switched design
 - No built in BDM header included, program via bed of nails or edge connector
 - Less spare and GP and diagnostic drivers and protection circuits
 - Less injector and ignition drivers, 4 minimum each, optimally 6 ignition, 8 injection

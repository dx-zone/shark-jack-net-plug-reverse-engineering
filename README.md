# 🔧 My Hak5 Shark Jack Repair & Reverse Engineering Project

**Device:** Hak5 Shark Jack — Battery Edition
**PCB:** NetPlug — 2019.07.02 — V1010
**Project started:** October 2026
**Last updated:** October 19, 2026
**Current status:** Troubleshooting and hardware investigation
**Inspection equipment:** Smartphone camera and LINKMICRO LM249MS digital microscope

------

## 1. 📖 Project Overview

### Why I started this project

My Hak5 Shark Jack was working normally until I attempted to update its firmware.

During the update, something went wrong. The firmware was being uploaded through the recovery web interface, but the process never completed.

After waiting several minutes without any progress, I discovered that the device had become completely unresponsive.

I tried powering it through different USB-C cables and power sources, but nothing seemed to bring it back to life.

There was no visible LED activity, and connecting the Ethernet interface didn't produce a network link.

At that point, I decided to take a different approach.

Instead of assuming the device was permanently damaged, I wanted to investigate what actually happened and determine whether I could recover it.

This project is my attempt to understand the Shark Jack's hardware, diagnose the failure, and hopefully restore it to working condition.

I'm also treating this as an opportunity to improve my electronics troubleshooting, PCB inspection, and hardware reverse-engineering skills.

### What I hope to accomplish

My main objective is to recover the Shark Jack. However, I want to go beyond simply getting it to boot.

I want to understand how the device works internally, including its processor, memory, power circuitry, and firmware storage.

I'll be investigating the following areas:

1. Identifying the major components on the PCB.
2. Understanding how power is distributed throughout the board.
3. Looking for physical damage or missing components.
4. Investigating possible UART debugging connections.
5. Determining whether the bootloader is still operational.
6. Identifying the flash memory and exploring recovery options.
7. Documenting measurements, experiments, discoveries, and repairs.

**My goal is to make decisions based on actual evidence rather than assumptions.**

------

## 2. ⚠️ How the Shark Jack Failed

### What happened during the firmware update

Before attempting the firmware update, the Shark Jack was functioning normally.

I followed the firmware update procedure and accessed the web interface used to upload the firmware.

The upload appeared to be progressing, but the process never finished.

After several minutes, the device stopped responding.

I couldn't tell whether the firmware upload had corrupted the bootloader, interrupted the normal boot process, or caused another problem.

What I could confirm was that the Shark Jack was no longer functioning as expected.

### Symptoms I observed

| Component or feature | What I observed                                          |
| -------------------- | -------------------------------------------------------- |
| Power                | The device no longer starts normally                     |
| LEDs                 | No visible activity                                      |
| Ethernet             | No network link detected                                 |
| USB-C                | Multiple cables and power sources tested                 |
| Firmware interface   | No longer accessible                                     |
| Battery              | Warmth observed near the battery during one powered test |
| Boot process         | Unknown                                                  |
| Bootloader           | Unknown                                                  |
| Firmware integrity   | Unknown                                                  |

At this stage, I don't have enough evidence to confirm that the firmware is the only problem.

Although the failure occurred during a firmware update, I still need to verify that the hardware is receiving the correct voltages and that the processor is capable of starting.

**Current conclusion:** I have a device that no longer boots or establishes an Ethernet connection. Firmware corruption is a strong possibility, but it remains unconfirmed.

------

# 3. 🔩 Opening the Shark Jack

## 3.1 Initial disassembly

After exhausting the basic recovery attempts, I decided to open the device to inspect the internal hardware.

The Shark Jack has a compact enclosure, so I carefully pried it open to expose the PCB and battery.

While peeling the adhesive-held battery away from the PCB, I discovered a tiny SMD component stuck to the battery adhesive. I suspect the adhesive may have lifted it from the board during disassembly, but I did not observe the exact moment it detached and still need to confirm its original position. This is a separate event from the firmware-update failure that prompted me to open the Shark Jack.

Once I had access to the internal components, I began photographing the board from multiple angles.

I wanted to preserve a visual reference of the component placement, wiring, solder joints, and overall condition before attempting any repairs.

These photographs became my initial documentation of the device's internal construction.

### Initial photographs

I captured 13 photographs during the initial disassembly.

They cover both sides of the PCB, the internal battery, the Ethernet wiring, the processor, and other components.

#### 📷 Initial disassembly overview

![Shark Jack initial disassembly 6489](media/initial-disassembly/shark-jack-initial-disassembly-6489.jpg)

**My notes:** This is one of my first photographs after opening the enclosure. It provides an overview of the internal PCB, Ethernet wiring, and USB-C connection.

------

#### 📷 PCB component-side overview

![Shark Jack initial disassembly 6490](media/initial-disassembly/shark-jack-initial-disassembly-6490.jpg)

**My notes:** This photograph gives me another reference for identifying components and understanding their placement on the board.

------

#### 📷 Battery and rear PCB

![Shark Jack initial disassembly 6491](media/initial-disassembly/shark-jack-initial-disassembly-6491.jpg)

**My notes:** I can use this photograph to document the battery position, insulation, wiring, and surrounding circuitry.

------

#### 📷 Ethernet connection and battery arrangement

![Shark Jack initial disassembly 6492](media/initial-disassembly/shark-jack-initial-disassembly-6492.jpg)

**My notes:** This image provides another angle of the battery and Ethernet connections. I'll use it when inspecting the wiring and solder joints.

------

#### 📷 Processor and nearby components

![Shark Jack initial disassembly 6493](media/initial-disassembly/shark-jack-initial-disassembly-6493.jpg)

**My notes:** This photograph provides a closer look at the main processor area and nearby surface-mounted components.

------

#### 📷 Additional IC and USB-C circuitry

![Shark Jack initial disassembly 6494](media/initial-disassembly/shark-jack-initial-disassembly-6494.jpg)

**My notes:** I captured this area to investigate the additional integrated circuit and the components closer to the USB-C end of the PCB.

------

#### 📷 Battery wiring and switch

![Shark Jack initial disassembly 6495](media/initial-disassembly/shark-jack-initial-disassembly-6495.jpg)

**My notes:** This view will help me trace the battery wiring and examine the physical switch arrangement.

------

#### 📷 PCB reverse side

![Shark Jack initial disassembly 6496](media/initial-disassembly/shark-jack-initial-disassembly-6496.jpg)

**My notes:** This photograph captures the opposite side of the PCB, including silkscreen markings and the switch area.

------

#### 📷 Additional reverse-side inspection

![Shark Jack initial disassembly 6497](media/initial-disassembly/shark-jack-initial-disassembly-6497.jpg)

**My notes:** I took this photograph from another angle to improve visibility of the PCB traces and surrounding components.

------

#### 📷 Detailed PCB and Ethernet wiring

![Shark Jack initial disassembly 6509](media/initial-disassembly/shark-jack-initial-disassembly-6509.jpg)

**My notes:** This photograph provides additional detail around the Ethernet wiring, component footprints, and solder connections.

------

#### 📷 Main processor and component markings

![Shark Jack initial disassembly 6510](media/initial-disassembly/shark-jack-initial-disassembly-6510.jpg)

**My notes:** This is one of the photographs I can use to identify the processor and other major components.

------

#### 📷 Internal battery

![Shark Jack initial disassembly 6511](media/initial-disassembly/shark-jack-initial-disassembly-6511.jpg)

**My notes:** This photograph documents the lithium-polymer battery, its insulation, and its position relative to the PCB.

------

#### 📷 PCB revision identification

![Shark Jack initial disassembly 6512](media/initial-disassembly/shark-jack-initial-disassembly-6512.jpg)

**My notes:** This view helps document the PCB markings, including the NetPlug identification and hardware revision.

------

# 4. 🧠 Identifying the Hardware

After opening the Shark Jack, I started identifying the components responsible for processing, networking, power management, and firmware storage.

The PCB contains several integrated circuits, passive components, switches, and connectors.

Based on the markings and photographs I've examined so far, I have the following preliminary hardware inventory.

| Component          | What I've identified                | Status                             |
| ------------------ | ----------------------------------- | ---------------------------------- |
| PCB                | NetPlug 2019.07.02 V1010            | ✅ Identified                       |
| Main processor     | MediaTek, likely MT7628 family      | 🔎 Exact model pending confirmation |
| Secondary IC       | Located near the main processor     | 🔎 Identification pending           |
| Flash storage      | Type and location not confirmed     | 🔎 Investigation pending            |
| Ethernet           | RJ45 connector with internal wiring | ✅ Identified                       |
| USB                | USB-C connector                     | ✅ Identified                       |
| Battery            | Internal lithium-polymer battery    | ✅ Identified                       |
| Crystal/oscillator | Component marked 40.000 MHz         | ✅ Marking observed                 |
| Slide switch       | Physical control switch             | ✅ Identified                       |
| UART interface     | Possible TX/RX/GND pads             | 🔎 Requires verification            |

### What I still need to determine

Although I can identify several major components visually, I haven't completed the electrical investigation.

I still need to identify the exact processor model, determine the type of flash memory being used, and locate the power-management circuitry.

I'm particularly interested in finding a serial debugging interface.

If I can establish a working UART connection, I may be able to observe what happens when the processor attempts to boot.

That information would be extremely valuable because it could help distinguish a firmware problem from a hardware problem.

------

# 5. 🔬 Inspecting the PCB With My LINKMICRO LM249MS

## 5.1 Why I decided to use a microscope

The initial smartphone photographs gave me a useful overview of the Shark Jack's internal construction.

However, I quickly realized that some of the components were too small to inspect properly using the phone camera alone.

I wanted to examine the solder joints, PCB traces, and surface-mounted components in much greater detail.

For this stage of the investigation, I used my **LINKMICRO LM249MS digital microscope**.

The microscope allows me to magnify the PCB and inspect areas that would otherwise be difficult to evaluate.

This is particularly useful when working with tiny SMD components and identifying potential physical damage.

### What I'm looking for

During my microscope inspections, I'm focusing on:

- Missing or displaced components.
- Damaged solder joints.
- Cracked ceramic capacitors.
- Broken or lifted PCB pads.
- Damaged traces.
- Solder bridges.
- Unpopulated component footprints.
- Signs of previous soldering or rework.

I also want to distinguish between intentional design features and actual damage.

An empty component footprint, for example, doesn't necessarily mean a component is missing.

Manufacturers often use the same PCB design for multiple configurations, leaving certain component positions unpopulated.

------

## 5.2 First microscope inspection

My first set of microscope photographs contains eight images.

These images focus on a particular section of the PCB containing several small SMD components, exposed pads, and traces.

I also photographed the tiny SMD component I found stuck to the battery adhesive while opening the device.

### Photograph 001 — First magnified PCB inspection

![Shark Jack LINKMICRO inspection 001](media/microscope/shark-jack-linkmicro-lm249ms-inspection-001.JPG)

**My observations:**

This photograph shows a section of the PCB near the NetPlug silkscreen marking.

Several small surface-mounted components are visible, along with traces and exposed pads.

I noticed that some component positions appear populated while others are empty.

At this point, I can't determine whether the empty positions are intentional or whether a component has become detached.

I'll need to compare this area with earlier photographs and examine the solder pads more closely.

------

### Photograph 002 — Closer inspection of SMD components

![Shark Jack LINKMICRO inspection 002](media/microscope/shark-jack-linkmicro-lm249ms-inspection-002.JPG)

**My observations:**

This photograph provides another view of the same general area.

The increased detail makes it easier to examine the tiny components and the traces connecting them.

I'm particularly interested in the arrangement of the unpopulated pads and whether they show signs of previously soldered components.

For now, I haven't identified conclusive evidence of a missing part at this location.

------

### Photograph 003 — Investigating a possible missing component location

![Shark Jack LINKMICRO inspection 003](media/microscope/shark-jack-linkmicro-lm249ms-inspection-003.JPG)

**My observations:**

In this photograph, I used the tip of my tweezers to point toward a suspicious area on the PCB.

Two exposed square pads caught my attention.

One possibility is that these pads belong to a component that was removed or became detached.

However, there are other explanations.

They could be test points or part of an intentionally unpopulated footprint.

I don't want to assume they represent damage without additional evidence.

**Next step:** I'll inspect this area again and compare it with the original disassembly photographs.

If necessary, I'll use my multimeter to investigate the electrical connections associated with these pads.

------

## 5.3 Investigating an SMD component found on the battery adhesive

When I peeled the battery away from the PCB during disassembly, I found a tiny SMD component stuck to its adhesive. This is how I discovered the component; it was not simply a loose part I found elsewhere on the workbench.

The component has a rectangular, tan-colored body with metallic ends. Its appearance suggests a multilayer ceramic capacitor (MLCC), but the identity is not yet fully confirmed.

I suspect the adhesive may have pulled the component from the PCB while I separated the battery. I did not witness the exact detachment, however, so I cannot yet say whether it came off during removal or had already been loose. Under the LINKMICRO LM249MS, I found a possible empty two-pad footprint worth investigating. Its location has **not** been confirmed as the component's original position.

If I identify the matching footprint and confirm that the pads and component are intact, I may need to solder it back in place. I will not attempt that until I verify where it belongs and check for shorts or damaged pads.

**📷 TODO — Photograph the component on the battery adhesive (if an image from the discovery exists)**

*Insert a photograph of the component where it was found, if available. Otherwise, retain this written observation as the original discovery record.*

### Photograph 004 — Loose SMD component

![Shark Jack LINKMICRO inspection 004](media/microscope/shark-jack-linkmicro-lm249ms-inspection-004.JPG)

**My observations:**

This photograph shows the loose component positioned near the tip of my tweezers.

The component is extremely small, making it difficult to inspect without magnification.

Its appearance is consistent with a ceramic capacitor, although visual appearance alone isn't sufficient to prove its identity.

------

### Photograph 005 — SMD component from another angle

![Shark Jack LINKMICRO inspection 005](media/microscope/shark-jack-linkmicro-lm249ms-inspection-005.JPG)

**My observations:**

I photographed the same component from another angle to get a better look at its body and terminals.

The metallic ends are visible.

Because I recovered this component from the battery adhesive during disassembly, I am investigating whether it came from a nearby PCB footprint.

However, I still need evidence connecting it to a particular PCB footprint.

------

### Photograph 006 — Component isolated on my work mat

![Shark Jack LINKMICRO inspection 006](media/microscope/shark-jack-linkmicro-lm249ms-inspection-006.JPG)

**My observations:**

I placed the component on my blue silicone work mat to inspect it independently from the PCB.

This makes it easier to examine its shape and condition without surrounding components obstructing the view.

I also want to measure its dimensions to estimate the SMD package size.

------

### Photograph 007 — Close-Up of the SMD Component Inside Its Protective Case

![Shark Jack LINKMICRO inspection 007](media/microscope/shark-jack-linkmicro-lm249ms-inspection-007.JPG)

**My observations:**

I placed the tiny SMD component inside a transparent protective case to prevent accidentally losing or damaging it.

Using my LINKMICRO LM249MS microscope, I captured a magnified view of the component and its metallic terminals through the clear case.

The component has not been conclusively identified, but its appearance and the 3.888 µF capacitance reading support the possibility that it is a ceramic capacitor.

------

### Photograph 008 — SMD Component Secured to an Adhesive Pad Inside Its Protective Case

![Shark Jack LINKMICRO inspection 008](media/microscope/shark-jack-linkmicro-lm249ms-inspection-008.JPG)

**My observations:**

This photograph shows the same SMD component from Photograph 007, secured to a small adhesive pad inside its transparent protective case.

Because the component is extremely small and easy to lose, I decided to store it this way until I'm ready to investigate its original location on the PCB.

The adhesive pad keeps the component from moving freely inside the case.

**Next step:** Once I identify and verify the suspected missing component footprint, I'll evaluate whether the component can be safely soldered back onto the PCB.

------

# 6. ⚡ Testing the Loose Component

After recovering the tiny SMD component from the battery adhesive, I tested it using my multimeter in capacitance mode. I recorded **3.888 µF (microfarads)**.

This reading supports my suspicion that the part is a capacitor, possibly an MLCC. It is near 3.9 µF, but I have not verified the manufacturer's nominal rating, voltage rating, or whether the component is electrically sound. I plan to repeat the measurement under controlled conditions and document the meter and test setup.

My working theory is that adhesive pulled a capacitor off the PCB as I removed the battery. The missing-pad location is still only a candidate, not a verified match. I must establish that match before attempting to solder the component back.

### Measurement record

| Property              | My findings                   |
| --------------------- | ----------------------------- |
| Component type        | Suspected ceramic capacitor   |
| Physical appearance   | Tan rectangular SMD component |
| Terminals             | Two metallic ends             |
| Initial measurement   | 3.888 µF                      |
| Nominal capacitance   | Unknown                       |
| SMD package           | Unknown                       |
| Original PCB location | Suspected two-pad footprint; unconfirmed |
| Component condition   | Not fully evaluated           |
| Storage | Clear protective case, secured to an adhesive pad (Photographs 007–008) |
| Where it was found | Stuck to battery adhesive during battery removal |
| Suspected detachment mechanism | Adhesive pulling the part from the PCB; unconfirmed |
| Possible repair | Resolder only if original footprint and component integrity are verified |

### What I plan to test next

Before attempting to reinstall this component, I want to repeat the capacitance measurement and inspect its body and terminals for damage.

I'll also inspect the PCB to determine whether any footprint matches the component's dimensions, solder residue, and electrical connections. I will disconnect power and take care around the lithium-polymer battery before any soldering work.

**I will not solder the component onto the PCB until I can reasonably establish where it belongs.**

Installing a capacitor across the wrong pads could damage the device or create an electrical short.

------

# 7. 🔋 Investigating the Power Circuit

One of my first priorities is understanding why the Shark Jack no longer powers up normally.

I know that the device stopped functioning during the firmware update, but I still need to determine whether its power circuitry is working.

I previously observed some warmth near the battery while the USB-C cable was connected.

However, this doesn't prove the battery was charging properly or that the PCB was receiving the required voltages.

I need actual electrical measurements.

## 7.1 Battery inspection

My first step will be to inspect the lithium-polymer battery and its connections.

I'll look for swelling, punctures, damaged insulation, loose wiring, or other signs of physical damage.

If the battery appears safe, I'll measure its voltage using my multimeter.

### Battery measurement

| Test                      | Result  |
| ------------------------- | ------- |
| Battery visual inspection | Pending |
| Battery voltage           | Pending |
| Battery wiring continuity | Pending |
| Charging behavior         | Pending |

**📷 IMAGE PLACEHOLDER — Battery and electrical measurement**

*Insert a photograph showing the battery connection points and voltage measurement.*

**My findings:** To be documented.

I won't attempt to charge or reuse a battery that shows signs of damage.

------

## 7.2 USB-C power input

Next, I'll investigate whether power from the USB-C connector reaches the PCB.

I want to verify the input voltage and determine whether the charging and power-management circuitry responds appropriately.

I'll also examine the connector's solder joints under the microscope.

### USB-C inspection

| Test                       | Result  |
| -------------------------- | ------- |
| USB-C connector condition  | Pending |
| USB input voltage          | Pending |
| USB current consumption    | Pending |
| Ground continuity          | Pending |
| Power-management circuitry | Pending |

**📷 IMAGE PLACEHOLDER — USB-C connector inspection**

*Insert a microscope photograph of the USB-C connector and surrounding circuitry.*

**My findings:** To be documented.

------

## 7.3 Checking regulated voltages

Once I confirm that USB power is reaching the board, I want to identify the voltage regulators and measure their outputs.

These components supply the operating voltages required by the processor, memory, and other circuitry.

If an essential power rail is missing, firmware recovery may not be possible until the electrical problem is resolved.

I plan to identify the relevant test points and record the voltage measurements.

**I won't assume the board uses a particular voltage rail until I have identified the relevant circuitry.**

### Power rail measurements

| Test point       | Expected voltage | Measured voltage | Status  |
| ---------------- | ---------------- | ---------------- | ------- |
| Battery          | To be determined | —                | Pending |
| USB input        | To be verified   | —                | Pending |
| Regulator 1      | Unknown          | —                | Pending |
| Regulator 2      | Unknown          | —                | Pending |
| Processor supply | Unknown          | —                | Pending |
| Memory supply    | Unknown          | —                | Pending |

**📷 IMAGE PLACEHOLDER — Voltage regulator investigation**

*Insert an annotated photograph identifying the regulator, ground reference, and measurement point.*

------

# 8. 🖥️ Investigating the UART Debugging Interface

One of the most interesting parts of this project is the possibility of accessing the Shark Jack's serial console.

During the PCB inspection, I noticed pads that may be associated with UART communication.

Some appear to have markings such as TX, RX, and GND.

If these pads are connected to the processor's serial interface, they could provide information about the boot process.

### Why UART matters

A working UART connection could help me determine:

- Whether the processor begins executing code.
- Whether a bootloader is present.
- Whether the operating system begins loading.
- Whether the firmware fails during startup.
- Whether a supported recovery mechanism is available.

If I can capture a boot log, I'll have much more useful information than I currently have.

## 8.1 My UART investigation plan

Before connecting anything, I'll identify the suspected serial pads and verify their electrical characteristics.

I need to establish the ground connection and determine the UART logic voltage.

I won't assume the interface operates at 3.3 volts simply because that voltage is common in embedded hardware.

Once the signal levels are known, I'll use a compatible USB-to-UART adapter.

I'll begin by connecting only the adapter's ground and receive input to the appropriate board signals.

I won't connect the adapter's power output to the Shark Jack.

My first objective is simply to listen for serial output during startup.

### UART investigation log

| Signal         | PCB location  | Voltage | Status  |
| -------------- | ------------- | ------- | ------- |
| GND            | Unknown       | —       | Pending |
| TX             | Suspected pad | Unknown | Pending |
| RX             | Suspected pad | Unknown | Pending |
| UART baud rate | Unknown       | —       | Pending |

**📷 IMAGE PLACEHOLDER — UART test pads**

*Insert an annotated microscope photograph showing the suspected UART connections.*

**My findings:** To be documented.

### Capturing the boot log

If I establish a working serial connection, I'll capture the entire startup sequence.

I'll preserve the original log before making any changes.

If nothing appears on the serial console, I'll investigate possible causes such as incorrect pin identification, incompatible voltage levels, incorrect communication settings, or a processor that isn't starting.

**No serial output wouldn't automatically prove that the bootloader is corrupted.**

------

# 9. 💾 Firmware and Flash Memory Recovery

If I confirm that the power circuitry is functioning, my next major objective will be investigating the firmware storage.

I want to identify the flash memory used by this Shark Jack and determine whether its contents can be recovered.

The firmware update failure makes corrupted flash contents a reasonable possibility.

However, I haven't established whether the bootloader, operating system, or another partition was affected.

## 9.1 Identifying the flash memory

I'll start by examining the integrated circuits on the PCB and recording their markings.

Once I identify the flash memory device, I'll look for its datasheet.

I want to determine:

- The memory manufacturer and model.
- The storage technology.
- The memory capacity.
- Its operating voltage.
- Its communication interface.
- Whether an external programmer can access it.

**📷 IMAGE PLACEHOLDER — Flash memory identification**

*Insert a microscope photograph showing the flash memory markings.*

**Component identification:** Pending.

------

## 9.2 Backing up the original firmware

If I can access the flash memory, my first goal will be to preserve its contents.

I don't want to overwrite potentially recoverable information.

Ideally, I'll create two independent copies of the original flash contents and compare their SHA-256 hashes.

If both backups match, I'll have greater confidence that the data was read consistently.

I'll keep those backups separate from any modified firmware images.

This is especially important because the flash may contain device-specific information such as configuration data, network addresses, or calibration values.

### Firmware backup log

| Property             | Result      |
| -------------------- | ----------- |
| Flash manufacturer   | Pending     |
| Flash model          | Pending     |
| Flash capacity       | Pending     |
| Flash interface      | Pending     |
| First backup         | Not created |
| Second backup        | Not created |
| SHA-256 verification | Pending     |

------

## 9.3 Investigating recovery options

Once I understand the bootloader and flash configuration, I'll evaluate the available recovery options.

I may be able to recover the device through its serial console, a supported recovery interface, or direct flash programming.

The best approach will depend on what I discover.

I don't want to erase or rewrite the flash memory before verifying the correct firmware image and storage layout.

My priority is to preserve recoverable information while minimizing the risk of additional damage.

------

# 10. 🔍 Possible Causes of the Failure

At this stage, I have several theories about what might have happened.

I want to keep them documented without treating any of them as confirmed.

| Possible problem            | Why I'm investigating it                      | Current status  |
| --------------------------- | --------------------------------------------- | --------------- |
| Corrupted firmware          | Failure occurred during firmware update       | Suspected       |
| Damaged bootloader          | Device stopped responding after failed upload | Unconfirmed     |
| Battery or charging problem | No normal power-up behavior                   | Not tested      |
| Missing power rail          | No LED or Ethernet activity                   | Not tested      |
| Detached SMD component      | Found stuck to battery adhesive during removal | Source footprint unconfirmed |
| Physical PCB damage         | Device was opened for inspection              | Not established |
| Flash memory failure        | Could prevent booting                         | Not tested      |
| Processor failure           | Could explain complete unresponsiveness       | No evidence yet |

The firmware failure remains my primary lead because the device was working before the update.

However, I want to verify the basic electrical conditions before attempting firmware recovery.

------

# 11. 🛠️ My Troubleshooting and Repair Plan

I want to approach this investigation systematically rather than randomly testing components or attempting repairs.

I've organized the next steps into phases.

## Phase 1 — Complete the visual inspection

- Photograph both sides of the PCB under the microscope.
- Identify the main integrated circuits.
- Inspect the power circuitry.
- Inspect the USB-C connector.
- Inspect the Ethernet wiring.
- Investigate the loose SMD component.
- Compare suspicious footprints against earlier photographs.
- Look for damaged traces or lifted solder pads.

**My objective:** Establish whether there is visible physical damage.

### Repair Task 001 — Identify the Suspected Detached SMD Component

**Status:** Open — no soldering performed  
**Discovery:** Found stuck to the battery adhesive during disassembly  
**Initial capacitance reading:** 3.888 µF (pending repeat measurement)  
**Storage:** Transparent protective case with an adhesive retention pad  
**Candidate PCB location:** An exposed two-pad footprint; not confirmed  
**Potential action:** Reinstall only after verifying the original footprint, component condition, and pad integrity

I want to use the original disassembly photos, microscope images, package dimensions, solder evidence, and electrical continuity measurements to evaluate the candidate footprint. I will record findings in `measurements/component-tests.md` and the chronology in `docs/repair-log.md`. I will disconnect all power sources and keep the lithium-polymer battery away from the rework area before applying heat.

## Phase 2 — Investigate the power circuitry

- Inspect the battery.
- Measure battery voltage.
- Verify USB-C input voltage.
- Measure USB current consumption.
- Identify voltage regulators.
- Measure regulated voltages.
- Check the slide switch.
- Investigate any abnormal electrical readings.

**My objective:** Determine whether the PCB receives the power required to operate.

## Phase 3 — Investigate boot activity

- Identify possible UART pads.
- Verify ground and signal voltage levels.
- Connect a compatible USB-to-UART adapter.
- Capture serial output during startup.
- Determine whether the bootloader responds.
- Preserve any boot logs.

**My objective:** Determine how far the device progresses through its startup process.

## Phase 4 — Investigate firmware storage

- Identify the flash memory.
- Locate its datasheet.
- Determine the flash interface.
- Investigate available read-only access methods.
- Back up the original contents if possible.
- Verify the backups.
- Determine the firmware layout.

**My objective:** Preserve the existing firmware and identify a safe recovery method.

## Phase 5 — Attempt recovery

- Obtain a firmware image verified for this hardware.
- Determine the appropriate recovery procedure.
- Attempt recovery using the least invasive supported method.
- Verify that the device boots.
- Test Ethernet connectivity.
- Confirm LED activity.
- Test normal USB and battery operation.
- Document the final results.

**My objective:** Restore the Shark Jack to a stable, working condition.

------

# 12. 📊 My Measurement and Experiment Log

I'll use this section to document measurements as the investigation progresses.

I want to record not only the results, but also the testing conditions and equipment used.

This will make it easier to reproduce experiments and identify patterns.

| Date                 | Component or test   | Measurement         | Result            |
| -------------------- | ------------------- | ------------------- | ----------------- |
| Before Oct. 19, 2026 | Loose SMD component | Capacitance         | 3.888 µF reported |
| Pending              | Battery             | DC voltage          | —                 |
| Pending              | USB-C               | Input voltage       | —                 |
| Pending              | USB-C               | Current consumption | —                 |
| Pending              | Voltage regulator   | Output voltage      | —                 |
| Pending              | UART TX             | Logic voltage       | —                 |
| Pending              | UART                | Boot output         | —                 |
| Pending              | Flash memory        | Identification      | —                 |

### My experiment notes

**Date:** ____________________

**Equipment used:** ____________________

**What I wanted to test:**

*Write my objective here.*

**Procedure:**

*Document exactly what I did.*

**Results:**

*Record measurements and observations.*

**What I learned:**

*Explain what the results suggest and what they do not establish.*

**Next step:**

*Document the next experiment.*

**📷 IMAGE PLACEHOLDER — Experiment evidence**

*Attach relevant microscope photographs, multimeter readings, or screenshots.*

------

# 13. 📁 Organizing My Project Files

I want to keep the documentation, photographs, measurements, and firmware information organized in a way that makes future investigations easier.

I'm using descriptive filenames so I can recognize photographs without opening each one.

## Photograph naming

For the original disassembly photographs, I'm using the following format:

```
shark-jack-initial-disassembly-6489.jpg
```

For the microscope photographs, I'm using:

```
shark-jack-linkmicro-lm249ms-inspection-001.JPG
```

This naming convention preserves the original image identifiers while making the purpose of each photograph easier to understand.

### My project directory

```text
Shark_Jack/
├── README.md
├── docs/
│   ├── diagnostics/
│   ├── firmware/
│   ├── hardware/
│   └── repair-log.md
├── firmware/
│   ├── backups/
│   ├── original/
│   └── recovered/
├── logs/
│   ├── diagnostics/
│   └── uart/
├── measurements/
├── media/
│   ├── annotated/
│   ├── initial-disassembly/
│   │   ├── shark-jack-initial-disassembly-6489.jpg
│   │   └── ...
│   └── microscope/
│       ├── shark-jack-linkmicro-lm249ms-inspection-001.JPG
│       └── ...
├── references/
│   └── datasheets/
└── scripts/
```

I'll keep the unedited JPEG documentation copies and the original microscope captures unchanged whenever possible. The original HEIC disassembly files have been replaced in the working tree by JPEG copies; earlier Git history may still contain the HEIC versions.

If I annotate an image to identify a component, trace, or measurement point, I'll save the annotated version separately.

The timestamps embedded in the LINKMICRO filenames should not be treated as confirmed capture dates because they may reflect the microscope's internal clock settings.

------

# 14. 📝 Project Progress and Discoveries

## October 2026 — Initial investigation

After the unsuccessful firmware update, I confirmed that the Shark Jack no longer exhibited normal LED or Ethernet activity.

I tested different USB-C cables and power sources without restoring normal operation.

I opened the enclosure to investigate the internal hardware and captured 13 photographs documenting the PCB, battery, and surrounding components.

## October 2026 — Battery removal observation

While peeling the battery off its adhesive, I discovered a small SMD component attached to the adhesive. I suspect it was pulled from the PCB, though its original location is not yet confirmed. I measured the recovered component at 3.888 µF and photographed it with the LINKMICRO microscope. Any possible resoldering will wait until I verify the correct footprint.

**Important timeline distinction:** The Shark Jack became unresponsive during the firmware update *before* I opened it. The possible component detachment happened or was discovered later, while separating the battery adhesive. I am investigating these as separate issues rather than treating the capacitor as the established cause of the initial failure.

## October 19, 2026 — Microscope inspection

I continued the investigation using my LINKMICRO LM249MS digital microscope.

I captured eight additional photographs focusing on small PCB components, exposed solder pads, and the SMD component found stuck to the battery adhesive.

The microscope images revealed several areas worth investigating further.

I documented that the component was found stuck to the battery adhesive while I peeled the battery away. I suspect the adhesive may have pulled it off the PCB, but I have not conclusively identified the original footprint or confirmed when detachment occurred.

At this point, the project is transitioning from visual inspection to electrical testing.

------

# 15. 🎯 Where I Stand Right Now

I've made progress understanding the Shark Jack's internal construction, but I haven't recovered the device yet.

I've documented both sides of the PCB, identified several major hardware components, and started investigating the smaller SMD components under magnification.

The SMD component I found stuck to the battery adhesive remains an open repair question. I have measured it at 3.888 µF and stored it in a protective case, but I have not confirmed its PCB footprint or whether it needs resoldering.

The firmware update failure is still the most significant clue, but I need electrical measurements before drawing conclusions.

My immediate priorities are to verify the power circuitry, identify the UART interface, and determine whether the processor produces any boot activity.

If the power rails are stable and the processor is responding, I'll focus more heavily on the firmware and flash memory.

If the electrical measurements reveal a hardware problem, I'll address that first.

### What I've confirmed

✅ The Shark Jack worked before the firmware update.

✅ The firmware update failed to complete.

✅ The device became unresponsive afterward.

✅ Normal LED and Ethernet activity are absent.

✅ I've opened the device and documented its PCB.

✅ The PCB is marked `NetPlug`, `2019.07.02`, and `V1010`.

✅ I've completed an initial LINKMICRO LM249MS inspection.

✅ I found an SMD component stuck to the battery adhesive during removal, measured 3.888 µF, photographed it, and stored it in a clear case on an adhesive pad.

### What I haven't confirmed

❌ Whether the bootloader is corrupted.

❌ Whether the processor is executing code.

❌ Whether all required voltage rails are present.

❌ Which PCB footprint, if any, the component found on the battery adhesive came from.

❌ Whether the flash memory can be accessed.

❌ Whether firmware recovery alone will restore the device.

------

# 16. 🏁 Final Thoughts

I started this project because I didn't want to discard a device simply because a firmware update had gone wrong.

The Shark Jack might have a corrupted bootloader, damaged firmware, an electrical problem, or some combination of issues.

I don't know yet.

What I do know is that I have an opportunity to learn something valuable by investigating it properly.

With my LINKMICRO LM249MS, multimeter, and other electronics tools, I can examine the hardware at a level that wasn't practical when I first purchased the device.

Even if the repair turns out to be more complicated than expected, I want this project to be worthwhile.

I'll continue documenting what I discover, including unsuccessful experiments, because understanding what doesn't work can be just as useful as understanding what does.

**My ultimate goal is to bring the Shark Jack back to life while building a better understanding of embedded electronics, firmware recovery, and hardware reverse engineering.**

------

**Project status:** 🔎 Investigation ongoing
**Next milestone:** ⚡ Electrical diagnostics and UART identification
**Last updated:** October 19, 2026
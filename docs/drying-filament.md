# Drying filament

This page is a practical note on drying FDM filament. It focuses on ABS, ASA, ABS-CF, ASA-CF, ABS-GF, ASA-GF, PC-CF, ezPC+CF, PC/ABS, PC/ASA, PA6, PA12, PA6-CF, PA12-CF, PA6-GF, and PA12-GF.

The main rule is simple. A dry purge should be boring. If the flow becomes uneven, foams, hisses, pops, or oozes as if it is still under pressure after retraction, the filament or the hotend system is not behaving like a stable melt.

## Table of contents

- [Introduction](#introduction)
- [Naming used here](#naming-used-here)
- [New filament is not guaranteed dry](#new-filament-is-not-guaranteed-dry)
- [What moisture does in the hotend](#what-moisture-does-in-the-hotend)
- [The boring purge test](#the-boring-purge-test)
- [Common failure modes](#common-failure-modes)
- [Failure modes in practice](#failure-modes-in-practice)
- [Material notes](#material-notes)
- [Drying temperatures](#drying-temperatures)
- [Why the spool matters](#why-the-spool-matters)
- [Drying equipment](#drying-equipment)
- [Practical workflow](#practical-workflow)
- [When a dried spool only prints well for a short time](#when-a-dried-spool-only-prints-well-for-a-short-time)
- [Troubleshooting](#troubleshooting)
- [Compact rules](#compact-rules)
- [References](#references)

## Introduction

Every filament benefits when moisture exposure is controlled. Some materials show only small changes. Others become unreliable very quickly.

The practical point is not that every spool must be treated like nylon. The point is that moisture makes printing less deterministic. A spool that printed cleanly yesterday can start stringing, flow unevenly, foam, or produce weaker parts after moisture exposure.

ABS and ASA are good examples. They are not usually the most moisture-critical FDM materials. Nylon, TPU, PC, and PC blends are usually more sensitive. Even so, ABS and ASA are hygroscopic enough that drying can improve consistency, surface quality, purge behavior, ooze control, and mechanical repeatability. Prusa notes that most FFF materials are hygroscopic, while also saying that some materials are affected more strongly than others, with polyamide as a strong example. [Prusa drying guide][prusa-drying]

A dry spool should extrude predictably. During a purge, the strand should have a mostly steady width and a smooth surface. When the same filament becomes wet, the purge can become uneven, foam, hiss, pop, ooze after retraction, string heavily, or produce weaker parts.

Filled versions such as ABS-CF, ASA-CF, ABS-GF, and ASA-GF still depend on the base polymer. Carbon fiber and glass fiber do not make the base polymer immune to moisture. Fillers can also make diagnosis harder because a partially restricted nozzle can look similar to wet filament during purge.

PC-CF, PC/ABS, PC/ASA, PA6, PA12, and fiber-filled PA6 or PA12 need stricter discipline. They can show both steam-related defects and chemical degradation during hot processing if moisture is present. That degradation can reduce molecular weight, lower melt viscosity, increase drooling, and reduce final part properties. [Toray ABS/PC guide][toray-abspc] [DuPont nylon guide][dupont-nylon]

## Naming used here

This page uses **PC-CF** as the generic name for carbon fiber reinforced polycarbonate.

Some vendors style this name differently. This page still uses PC-CF consistently. The general moisture behavior is similar, but drying temperature can be very different between products. For example, Prusa lists its PC-CF material at 95 °C for 4 hours, while 3DXTech lists CarbonX PC+CF at 120 °C for 4 hours. [Prusa drying guide][prusa-drying] [3DXTech drying instructions][3dxtech-drying]

This page uses **ezPC+CF** only for the specific 3DXTech CarbonX ezPC+CF product. Its official drying recommendation is lower than regular CarbonX PC+CF, at 80 °C for 4 hours. [3DXTech ezPC+CF][3dxtech-ezpc-cf]

Material names are broad categories, not exact recipes. ABS from one manufacturer is not necessarily the same as ABS from another. The same is true for ASA, PC-CF, PC blends, and nylons. Additives, impact modifiers, flame retardants, plasticizers, carbon fiber, glass fiber, processing aids, colorants, and the exact base resin can all change drying behavior, softening behavior, flow, stringing, bed adhesion, and chamber requirements.

Even different colors of the same filament line can behave differently. Pigments and additives can change flow, opacity, thermal behavior, and how clearly the material shows moisture defects. Treat the manufacturer's data sheet as the starting point, then validate the exact spool with purge behavior, print behavior, and drying tests.

## New filament is not guaranteed dry

A sealed factory bag is good storage. It is not proof that the filament is dry enough for best results.

There are three reasons for this.

First, filament production often uses water cooling after extrusion and before winding. Prusament describes its process as melted plastic leaving the die and immediately entering cooling baths. Industrial filament extrusion lines from Labtech and BOCO also describe water cooling or cooling tanks before winding. [Prusament how it is made][prusament-made] [Labtech extrusion line][labtech-line] [BOCO extrusion line][boco-line]

Second, factory drying, packaging quality, spool type, and storage history vary by manufacturer and material. Some filament arrives in excellent condition. Some arrives printable but not ideal. Some engineering materials may need drying before the first serious print.

Third, a desiccant packet in a sealed bag is mostly a storage aid. It helps keep dry filament dry. It does not reliably deep-dry a wet spool, especially when the filament is tightly wound and moisture is inside the filament or trapped deep in the spool.

3DGence makes the practical point directly. Tight factory packaging does not prove the material stayed dry, and they recommend assuming new material may need drying according to the manufacturer's recommendation. [3DGence drying note][3dgence-drying]

Water cooling during manufacturing does not prove that every new spool is wet. A good manufacturer can dry, handle, and package filament well after production. The safer rule is this.

- For PLA, PETG, ABS, and ASA, try it first if the print is not critical and the purge is boring.
- For ABS, ASA, and filled variants, dry when chasing repeatability.
- For PC-CF, PC/ABS, PC/ASA, PA6, PA12, PA6-CF, PA12-CF, PA6-GF, PA12-GF, and TPU, assume drying may be needed even for a new spool.
- For expensive or long prints, dry first and print from a dry box.

## What moisture does in the hotend

Moisture causes two main problems.

### Steam and gas pressure

Absorbed water travels with the filament into the hotend and flashes into steam. That gas expands inside the molten polymer. The result is not a stable melt. It is a gas-charged melt.

That can cause:

- bubbles in the purge strand
- popping or hissing
- surge-like extrusion
- rough or foamy surfaces
- blobs and zits
- stringing
- ooze that continues after retraction
- poor layer bonding

Bambu Lab describes the same basic mechanism in its drying guide. Moisture vaporizes inside the hot nozzle, which makes the molten filament expand and extrude irregularly. [Bambu drying recommendations][bambu-drying]

### Hydrolysis and lower melt viscosity

Some polymers do not merely carry moisture into the hotend. They can be chemically damaged when heated wet. This is hydrolysis.

This matters most for materials such as PC, PC/ABS, PC/ASA, PA, PET, PBT, and similar engineering polymers. Toray's ABS/PC processing guide states that insufficient drying of PC type resin can induce hydrolysis. The same guide connects this with molecular weight decrease, melt viscosity decrease, drooling, gas, silver streaks, odor, and reduced strength. [Toray ABS/PC guide][toray-abspc]

DuPont's nylon molding guide says excess moisture in nylon can cause hydrolysis, lower part toughness and strength, increased melt flow, lower melt viscosity, splay marks, and internal bubbles. [DuPont nylon guide][dupont-nylon]

For ABS and ASA, the main practical problem is usually steam and unstable extrusion rather than strong hydrolysis. That does not mean they never need drying. It means the failure mode is often less chemically destructive than PC or PA.

## The boring purge test

A simple purge check is useful.

Load filament, heat to normal print temperature, then purge a decent length at a steady feed rate. For example, push 30 to 50 cm of filament through a 0.5 mm nozzle. Watch the strand and listen.

A dry, clean, stable setup should look boring:

- mostly steady strand width
- smooth surface
- predictable curl
- little or no popping
- little or no uneven flow
- normal ooze for that material and temperature

A wet or unstable setup often looks active:

- alternating thick and thin sections
- random swelling
- small bubbles or craters
- rough or foamy surface
- hissing or popping
- drool that keeps growing after retraction
- visible vapor in severe cases

The 5 mm backoff check is also useful. Retraction can pull back filament and reduce mechanical pressure. It cannot remove steam bubbles that are already in the melt zone. If the hotend keeps oozing as if it has internal pressure after a large retract, moisture is a strong suspect.

This is not absolute proof. A partial clog, carbon fiber debris, glass fiber debris, extruder slip, spool drag, or incorrect temperature can also make extrusion inconsistent. The pattern helps.

Irregular flow with bubbles points toward moisture. A regular repeating pattern points more toward a mechanical or flow restriction issue.

## Common failure modes

| Symptom | What it can look like | Likely mechanism | Notes |
|---|---|---|---|
| Uneven purge flow | Strand width changes while feed rate is steady | Steam bubbles, unstable melt pressure, partial clog, or extruder slip | If drying fixes it, moisture was likely involved |
| Continued ooze after retraction | A blob keeps growing after a 5 mm retract | Steam pressure in the melt zone, sometimes amplified by lower viscosity | Dry material can ooze, but it should not feel pressure-driven after retraction |
| Nozzle-carried strings followed by a crash | Ooze forms dangling strings; the nozzle collects them, drops blobs, and later hits raised debris | Moisture-driven ooze, unstable melt, excessive temperature, or nozzle restriction | Common with insufficiently dried PC-CF and PC blends. The layer shift itself comes from lost position after a crash; wet filament can be an earlier cause of the buildup |
| Popping or hissing | Small crackles during loading, purge, or print | Water flashing into steam | Strong moisture indicator |
| Bubbles in purge | Foamy strand, craters, swelling | Steam bubbles escaping through the nozzle | Prusa lists bubbling during extrusion as a moisture symptom |
| Rough or matte surfaces | Print looks furry, foamed, cloudy, or inconsistent | Gas in the melt and unstable flow | Can also happen from wrong temperature or poor cooling |
| Stringing | Fine hairs between travel moves | Lower effective viscosity, steam expansion, or normal material behavior | Some materials string even when dry, compare before and after drying |
| Blobs and zits | Random raised defects on walls | Pressure surges or gas release | Also check seams, pressure advance, and retraction |
| Poor layer adhesion | Parts split more easily than expected | Voids, steam, degraded polymer, or poor temperature | Prusa lists low layer adhesion as a moisture-related symptom |
| Silver streaks, splay, or FDM foaming | Molding may show silver streaks or splay. FDM may show whitish hairs, rough extrusion, bubbles, foamy purge, or torn-looking infill | Moisture, gas in the melt, or hydrolysis in sensitive polymers | Do not expect FDM to look exactly like injection molding defects. The root cause can still be similar |
| Material becomes runny | More drool, more stringing, lower resistance to flow | Hydrolysis can lower molecular weight and melt viscosity | More relevant for PC, PC/ABS, PC/ASA, PA, PET, and PBT |
| Short good print window | First hours print well, later hours go bad | Outer wraps dried but inner wraps stayed wetter, or filament reabsorbs moisture during the print | See the dedicated section below |
| No improvement after drying | Same defects after a good dry cycle | Clog, worn nozzle, extruder issue, wrong temperature, bad filament diameter, or degraded material | Do a clean nozzle test before treating moisture as the only cause |


## Failure modes in practice

Wet filament does not always fail as one obvious defect. It often starts as a small extrusion problem and then turns into a mechanical print failure.

A useful diagnostic chain is:

1. What does the hotend do during purge?
2. What does the nozzle do during travel?
3. What gets left on the print?
4. What does the nozzle hit later?
5. Does drying change the behavior?

### Non-stop ooze after retraction

A useful warning sign is filament that keeps coming out of the nozzle during or after retraction.

Dry filament can still ooze at print temperature. That alone is normal. The warning sign is when the ooze behaves like it is being pushed from inside the hotend.

Typical signs:

- the nozzle keeps growing a blob after a large retract
- the ooze forms thin dangling strings
- the strand looks foamy, rough, swollen, or uneven
- wiping the nozzle does not stop the next blob from forming
- the behavior improves a lot after proper drying

Likely causes:

- water flashing into steam inside the melt zone
- gas pressure pushing molten polymer out of the nozzle
- lower melt viscosity from hydrolysis in moisture-sensitive polymers
- too high nozzle temperature
- over-priming during load
- partial nozzle restriction creating pressure buildup

In PC blends, PC-CF, PA6, PA12, and related materials, moisture can do more than create steam. It can also contribute to hydrolysis during hot processing. That can make the melt flow more easily and make printed parts weaker. [Toray ABS/PC guide][toray-abspc] [DuPont nylon guide][dupont-nylon]

### Dangling strings on the nozzle

Wet or unstable filament can produce strings that do not simply stay on the print. They can remain attached to the nozzle.

This can happen during:

- travel moves
- infill moves
- long moves between multiple objects
- combing or crossing over sparse infill
- pauses, tool changes, or filament load routines

The nozzle then acts like a hot collector. It drags strings around, melts them again, and sometimes drops them elsewhere.

This is one reason wet filament can seem to fail randomly. The defect may start in one area, but the nozzle can carry the material and deposit it somewhere else.

### Hairy or torn sparse infill

Sparse infill is often where wet PC-CF or PC blend filament first looks really bad.

The infill may look like:

- torn cloth
- raised hairs
- fuzzy fibers
- whitish wisps
- rough or foamed strands
- broken or dragged lines
- small curled spikes standing upward

This is not exactly the same as the injection molding defect called silver streaking. Silver streaking is a molding term for surface streak defects caused by gas, moisture, or degradation. In FDM, the related failure often appears as stringing, foaming, rough extrusion, weak infill, and nozzle buildup. [Toray ABS/PC guide][toray-abspc]

Sparse infill shows the problem early because it has many exposed lines, travel moves, gaps, speed changes, and unsupported spans. Walls may still look acceptable because each line is pressed into neighboring material. Infill has less support and gives unstable extrusion more room to misbehave.

### Raised debris and nozzle crash

This is the failure chain seen with insufficiently dried ezPC+CF and Add:north PC Blend HT LCF:

1. The filament is not dry enough.
2. The hotend keeps oozing during travel and after retraction.
3. Dangling strings form on the nozzle.
4. The nozzle drags those strings around the print.
5. Some strings are left across sparse infill or between parts.
6. The nozzle picks up more material and builds a blob.
7. The blob eventually drops onto the print or hardens on the nozzle.
8. The deposited material creates a raised feature.
9. On a later pass, the nozzle hits that raised feature.
10. The impact makes the motion system skip steps, which shifts subsequent layers.
11. The print is ruined.

This kind of failure can look like a motion problem at the end, but the original cause may have been unstable extrusion.

The visible layer shift is real, but it is secondary. It appears after the motion system loses position during the crash. The raised obstacle existed because the nozzle had been collecting and redepositing strings, blobs, or foamed material.

### Whitish hairs on dark PC-CF or PC blend filament

White or grey hairs on a dark filled filament do not automatically mean silver streaking.

More likely explanations are:

- tiny bubbles or voids scattering light
- foamed polymer looking lighter than solid polymer
- thin stretched strings looking pale under light
- stress-whitened or torn polymer
- rough fiber-filled extrusion with poor matrix flow
- dragged semi-solid material stretched by the nozzle

With carbon-filled filament, the apparent surface color can be misleading. A thin wisp can look much lighter than a solid extruded line.

### Uneven purge flow

A dry purge should be boring. When feeding filament at a steady rate through a clean nozzle, the strand should have mostly stable width and surface texture.

Wet or unstable filament may show:

- random thick and thin sections
- swollen sections
- small bubbles
- rough texture
- little craters
- sudden flow surges
- weak flow followed by a surge

Irregular flow with bubbles or crackling points toward moisture.

A regular repeating pattern may point more toward a mechanical issue, such as:

- extruder gear slip
- inconsistent filament diameter
- spool drag
- partial nozzle restriction
- debris from carbon fiber or glass fiber filament
- purge speed above what the hotend can melt consistently

### Blobs, zits, and raised debris

Moisture can cause blobs because steam creates pressure changes in the melt. The nozzle can extrude more material than expected even when the extruder motion is correct.

Blobs can also come from slicer settings, pressure advance, seam placement, temperature, retraction, or flow calibration. Moisture becomes more likely when blobs are combined with bubbling, rough purge, non-stop ooze, or major improvement after drying.

The dangerous version is not just a cosmetic blob. It is a raised lump that the nozzle can hit later. That can turn a moisture problem into a collision, skipped steps, and then a layer shift.

### Poor layer bonding

Wet filament can create weak bonding for several reasons:

- gas bubbles create voids
- foamed extrusion reduces contact area
- unstable flow makes line width inconsistent
- hydrolysis can weaken sensitive polymers
- the operator may lower temperature to fight ooze, then underheat the dry material

Poor layer bonding is especially important for PC blends and nylons because the part may look acceptable but fail mechanically.

### Failure during multi-part prints

Printing multiple objects can make wet-filament behavior worse.

There are more travel moves, more opportunities to string between parts, and more chances for the nozzle to carry material from one part to another. A small dangling string that would be harmless on a single object can become a hard blob when the nozzle drags it across several parts.

If multi-part prints fail but single-object prints are acceptable, check:

- travel stringing between objects
- nozzle buildup
- wipe behavior
- Z-hop
- print order
- chamber temperature
- whether the filament is being printed from a dry box

### What confirms moisture as the cause

Moisture is likely when several of these are true:

- purge flow becomes boring after drying
- non-stop ooze is reduced after drying
- bubbles or crackling disappear after drying
- infill hairs stop forming after drying
- the same G-code works after drying
- weight loss during drying is measurable
- the problem returns after the spool sits in open air

Moisture is less likely when:

- drying makes no difference
- the uneven flow is perfectly regular
- the nozzle curls extrusion hard to one side
- a nozzle swap fixes the issue
- the failure happens at the same height every time
- the extruder shows visible slipping or grinding
- the spool has high drag or tangles

### Practical note

For PC-CF and PC blend filament, do not treat hairy infill, non-stop ooze, and nozzle buildup as just a retraction tuning problem.

Retraction can reduce mechanical pressure from the extruder. It cannot remove steam bubbles already in the melt zone. It also cannot fix a polymer melt that has become too fluid or unstable because the material was processed wet.

The fix is usually a combination of:

- dry the spool more completely
- verify real dryer temperature with thermocouples
- use an open, heat-safe spool
- print from a dry box for long prints
- clean or replace the nozzle
- then tune temperature, retraction, wipe, and travel behavior

## Material notes

### ABS

ABS is hygroscopic, but in practical FDM use it is usually less moisture-critical than nylon, TPU, PC, and PC blends.

That does not mean ABS should be ignored. Wet ABS can still ooze, string, show surge-like purge flow, make popping sounds during extrusion, produce rougher surfaces, and produce weaker or less repeatable parts.

A useful way to think about ABS:

- It may not fail as dramatically as wet nylon.
- It can still become less deterministic.
- Drying can improve repeatability even when the spool was technically printable.
- A good ABS purge should still be boring.

3DXTech lists ABS at 80 °C for 4 hours in its general drying chart. This is a good starting point for regular ABS when the spool and filament can tolerate that temperature. [3DXTech drying instructions][3dxtech-drying]

ABS moisture has also been studied directly in FFF. A 2023 study on natural moisture in ABS filament found that increased moisture negatively affected tensile strength, dimensional accuracy, and surface structure of printed parts. [Hamrol ABS moisture study][hamrol-abs]

### ABS-CF and ABS-GF

Use the ABS drying recommendation unless the filament maker gives a different one.

The carbon or glass fiber changes stiffness, abrasion, and flow, but the base polymer still carries the moisture behavior. Filled ABS may hide some surface defects because of its matte finish, but it can still show bubbles, uneven flow, ooze, and inconsistent extrusion.

Filled ABS can make troubleshooting harder. Carbon fiber and glass fiber increase the chance of nozzle restriction, especially with smaller nozzles or contaminated material. If uneven purge flow remains after drying, check the nozzle before increasing drying time further.

### ASA

ASA is similar to ABS for drying purposes. It is hygroscopic enough to matter, but it is not usually treated as aggressively as nylon or PC.

Wet ASA can still become less predictable. It may show stringing, unstable purge flow, bubbles, rough surfaces, blobs, and weaker layer bonding. Drying ASA is often less about making an unusable material printable and more about making the process repeatable.

Prusa and 3DXTech both list ASA at 80 °C for 4 hours. [Prusa drying guide][prusa-drying] [3DXTech drying instructions][3dxtech-drying]

### ASA-CF and ASA-GF

Treat these as ASA first, then adjust based on the manufacturer's data.

Carbon fiber and glass fiber do not remove the need to dry the base polymer. CF and GF grades can also hide some surface symptoms because the finish is already textured or matte. Do not assume a clean-looking matte surface means the filament is dry.

If ASA-CF or ASA-GF purges with random swelling, bubbles, popping, or non-stop ooze after retraction, moisture is still a strong suspect. If the uneven flow follows a regular repeating pattern or does not improve after drying, check nozzle restriction, extruder grip, spool drag, and purge speed.

### ezPC+CF

ezPC+CF does not use the same drying recommendation as regular PC-CF.

3DXTech lists CarbonX ezPC+CF at 80 °C for 4 hours. It also lists the print temperature range as 260 to 280 °C and says a heated chamber is not required. [3DXTech ezPC+CF][3dxtech-ezpc-cf]

A true 85 to 90 °C forced air cycle can be a reasonable experiment when the material is not getting dry enough at the official setting, especially on a heat-safe open metal spool. Do not jump straight to 110 or 120 °C unless the filament maker allows it or you have tested a sacrificial sample.

### PC-CF

PC-CF drying temperature depends on the exact formulation.

Prusa lists its PC-CF material at 95 °C for 4 hours. 3DXTech lists CarbonX PC+CF at 120 °C for 4 hours. Both are PC-CF products, but the drying recommendations are not the same. [Prusa drying guide][prusa-drying] [3DXTech drying instructions][3dxtech-drying]

The safe rule is to follow the product data sheet first. If a PC-CF product specifies 120 °C and your dryer only reaches 90 °C, it may still improve the spool, but it may not fully dry it in a predictable time.

### PC/ABS and PC/ASA

PC blends can be moisture sensitive because the PC part of the blend can hydrolyze when heated wet. 3DXTech lists PC/ABS and PC/ASA at 110 °C for 4 hours in its general drying chart. [3DXTech drying instructions][3dxtech-drying]

Toray's ABS/PC guide is worth reading because it connects insufficient drying with hydrolysis, lower molecular weight, lower melt viscosity, drooling, gas, silver streaks, and lower strength. [Toray ABS/PC guide][toray-abspc]

### PA6, PA12, and filled nylon variants

Nylons are strongly hygroscopic. They can absorb moisture quickly enough that drying once and then printing from open air may not be enough for long prints.

For useful drying guidance, identify the nylon family instead of only saying that it is carbon-filled or glass-filled nylon. PA6, PA12, PA11, and other nylon grades do not absorb moisture at exactly the same rate and may have different drying recommendations.

For this page, the useful labels are PA6, PA12, PA6-CF, PA12-CF, PA6-GF, and PA12-GF. PA6 is usually more moisture sensitive than PA12, but both need drying discipline. Fiber-filled nylon still needs drying because the base polymer is still nylon.

3DXTech lists nylon at 90 °C for at least 4 hours, but also notes that saturated nylon may need 24 or more hours. Prusa lists PA11-CF at 90 °C for 6 hours and recommends keeping it in a dry box between uses. [3DXTech drying instructions][3dxtech-drying] [Prusa drying guide][prusa-drying]

## Drying temperatures

Always check the filament manufacturer's recommendation. The table below is a starting point, not a universal rule.

| Material | Starting point | Notes |
|---|---:|---|
| ABS | 80 °C, 4 h | 3DXTech general chart |
| ABS-CF, ABS-GF | Start from ABS spec | Use maker data if different |
| ASA | 80 °C, 4 h | Prusa and 3DXTech list this value |
| ASA-CF, ASA-GF | Start from ASA spec | Fiber does not remove moisture risk |
| ezPC+CF | 80 °C, 4 h | Official 3DXTech recommendation |
| PC-CF | 95 to 120 °C, 4 h | Prusa PC-CF is 95 °C, CarbonX PC+CF is 120 °C |
| PC/ABS, PC/ASA | Around 110 °C, 4 h | 3DXTech general chart |
| PA6, PA12, PA6-CF, PA12-CF, PA6-GF, PA12-GF | Often 80 to 90 °C, 4 h or more | Saturated nylon can need much longer. Check the exact nylon grade |
| PA11-CF | 90 °C, 6 h | Prusa recommendation |
| PETG | 55 to 65 °C, 4 to 6 h | Included for comparison |
| PLA | 45 to 65 °C depending on product | Included for comparison, avoid overheating |

Higher temperature is not automatically better. Too much heat can soften filament, fuse loops together, deform the spool, damage adhesives, or accelerate aging. When a spool is still wet, extending time is usually safer than raising temperature past the product recommendation.

3DXTech specifically warns not to exceed its maximum drying temperature because doing so can deform the filament, reel, or both. [3DXTech drying instructions][3dxtech-drying]

## Why the spool matters

A dryer can only dry the filament that actually sees hot, dry, moving air.

Many spools are poor drying fixtures. They may have:

- solid side walls
- a restrictive hub
- a cardboard center that blocks airflow
- a plastic core that deforms at drying temperature
- glue or press-fit parts that loosen when heated
- low-temperature plastic sides such as HIPS

The middle part of the spool is usually called the **spool hub** or **spool core**. Even if the outer sides have holes, the hub can still block airflow through the center of the filament pack.

This matters because drying a wound spool is not the same as drying a loose strand. The outer wraps heat up and lose water first. Inner wraps dry more slowly. A restrictive hub makes that worse.

Prusa gives a clear example of spool limits. Their older black plastic spool sides can loosen after heating above 45 °C. Their grey spool glue is listed as able to withstand up to 90 °C. Prusa also warns not to exceed drying temperature because filament can soften and stick together. [Prusa drying guide][prusa-drying]

Some high-temperature filaments are sold on spools that cannot survive the filament's ideal drying cycle. A practical example from the setup that prompted these notes was Add:north PC Blend HT LCF supplied on a HIPS spool that deformed badly above roughly 80 °C. Treat that as a spool-specific warning, not a guarantee that every current Add:north spool is the same. Check the actual spool material and temperature rating before using a hot drying cycle.

If the spool cannot survive the drying temperature, respool first. For demanding materials, the spool rating is part of the drying plan.

A good drying spool has:

- metal sides
- large side cutouts
- an open hub or spacer-style center
- no low-temperature glue dependency
- enough stiffness to survive respooling
- temperature headroom for 90 to 120 °C drying

Hexaxes DryAF is a commercial example of this idea. It uses aluminium discs, aluminium spacers, and an open-frame design intended to improve airflow and drying performance. Hexaxes lists a maximum working temperature of 300 °C. [Hexaxes DryAF][hexaxes-dryaf]

An open aluminium spool with large side cutouts and six spacer posts in the hub is close to ideal for drying because hot air can reach both sides and the center. It still does not make drying instant. Moisture must diffuse out from the filament and through the wound pack.

## Drying equipment

### Consumer filament dryers

Small filament dryers are useful for storage, low-temperature materials, and printing from a warm box. They can struggle with PC-CF, nylons, and materials that need 90 to 120 °C.

The displayed temperature is not always the filament temperature. Uneven heating is common. If the box claims 100 or 110 °C, verify it with thermocouples before trusting it.

### Food or mushroom dehydrators

A tunnel-style dehydrator with a large rear fan can work well when it reaches the needed temperature. It can be better than many consumer filament dryers because it moves a lot of air and has an exhaust path.

For ezPC+CF, a true 85 to 90 °C forced air dehydrator with venting and an open metal spool is a plausible drying setup. The official 3DXTech recommendation is 80 °C for 4 hours, but a wet spool may need longer. Think 8 to 12 hours if the spool has been wet for a long time, then verify by purge behavior and weight.

The important requirements are:

- true air temperature at the spool
- airflow through the sides and hub
- moisture leaving the chamber
- a spool that survives the temperature
- cooling in a sealed dry box or bag

Do not rely only on an IR camera when measuring aluminium. Shiny metal has low emissivity, so the reading can be wrong or can reflect nearby objects. Use a K-type thermocouple, or put high-emissivity tape on the metal and measure the tape. [FLIR emissivity note][flir-emissivity]

### Forced air lab ovens

A forced air lab oven is the repeatable option. It gives better temperature control, airflow, and often an exhaust flap. It is also larger and more expensive.

For small spaces, compact 15 to 23 L forced air ovens are worth looking at. The key requirements are:

- 230 V support in the EU
- forced convection
- stable control at 80 to 120 °C
- enough internal clearance for the spool
- an over-temperature safety device
- a way for moisture to leave the chamber

A natural convection mini oven can still work, but it usually needs longer drying and more verification.

### Dry boxes during printing

Drying and printing are different problems.

A dryer removes moisture from the spool. A dry box prevents the filament from taking moisture back up during the print.

For long prints with PC-CF, PC/ABS, PC/ASA, PA6, PA12, PA6-CF, PA12-CF, PA6-GF, and PA12-GF, print from a sealed dry box if possible. Use a PTFE feedthrough, rollers or a low-friction spool holder, a hygrometer, and a meaningful amount of desiccant.

The dry box does not need to be at 90 °C during printing. It needs to keep the filament away from room air.

## Practical workflow

### 0. Decide how strict the job needs to be

Not every print needs the same drying discipline.

A quick ABS or ASA bracket may be fine straight from storage. A long enclosed ASA-CF print, a functional ABS part, a PC-CF part, or a nylon part benefits from drying as part of process control.

A useful split:

- Casual print: print if purge is boring and surface quality is acceptable.
- Repeatable print: dry first, then store properly.
- Long or expensive print: dry first and print from a dry box.
- Nylon or PC-based print: assume moisture control is part of the material profile.

### 1. Check the material data sheet

Start with the filament maker's drying recommendation. Do not assume that all PC-CF needs the same temperature. ezPC+CF and regular CarbonX PC+CF are a good example of why this is wrong.

### 2. Check the spool before heating

Before drying, ask whether the spool can survive the drying cycle.

If the spool is cardboard, HIPS, unknown plastic, or has a restrictive hub, consider respooling to a metal open-hub spool. This is especially important for material that requires 90 °C or more.

### 3. Measure real temperature

Put a thermocouple near the spool. Better, use two or three probes:

- one in the air stream
- one near the outer wraps
- one near the hub or inner wraps

Let the dryer stabilize. Do not assume the display temperature is the actual filament temperature.

### 4. Use airflow and venting

Hot still air is weaker than hot moving air. A dryer also needs a way to get moisture out.

A small exhaust path is useful. Do not open the chamber so much that temperature collapses, but do not trap all the humid air inside.

### 5. Dry by result, not only by time

The listed time is a starting point. A very wet spool can need longer.

Good ways to check progress:

- weigh the spool before and after drying
- repeat drying until mass loss becomes small
- purge at the same temperature and compare behavior
- look for the boring purge
- run the same test print before and after drying

A 0.1 g scale can show useful trends. A 0.01 g scale is better.

### 6. Cool sealed

After drying, do not leave the hot spool on the bench. Hot dry filament in room air can start absorbing moisture again while it cools.

Move it into a sealed dry box, dry bag, or container with desiccant.

### 7. Print from a dry box for long jobs

This matters most for nylon and PC-based materials. If the job is long, drying before printing may not be enough.

## When a dried spool only prints well for a short time

A spool that prints well for only a few hours after drying is giving useful information.

The most likely explanations are below.

### The spool was not dried all the way through

The outer wraps may dry enough to print well. The inner wraps may remain wetter. After a few hours of printing, the filament path reaches wetter material and the print quality falls apart.

This can happen even with a good dryer. A wound spool is a thick mass of plastic. An open metal spool helps a lot, but it does not make drying instant.

### The filament reabsorbs moisture during the print

If the spool is dry but printed from room air, hygroscopic materials can pick up moisture during long jobs. Nylon is the obvious case, but PC-based materials can also be affected.

This is why a dry box is part of the workflow for long prints.

### The displayed dryer temperature was not the spool temperature

The chamber may read 90 °C while the inner wraps sit much cooler. This is common in small boxes and poorly ventilated dryers.

Measure with thermocouples before changing the material profile.

### The cause is not moisture

If the failure repeats at the same time or layer height, check heat creep, nozzle restriction, extruder temperature, spool drag, chamber temperature, and part cooling.

Moisture is common, but it is not the only cause of late print failure.

## Troubleshooting

### Drying improves purge but not the print

Check the dry box and feed path. The spool may be dry, but the filament may sit in room air before reaching the printer.

Also check print temperature. Wet filament often encourages people to lower temperature to reduce ooze, then the dry filament becomes underheated.

### Drying does not change uneven purge flow

Swap or clean the nozzle. CF and GF materials can carry debris or leave residue. A partial restriction can create pressure buildup and release behavior that looks like moisture-related surging.

Also check extruder grip, filament diameter, spool drag, and whether the purge speed is too high for the hotend.

### Filament oozes even when dry

Some ooze is normal at print temperature. Dry PC-CF, ABS, and ASA are still molten polymers. The warning sign is not any ooze. The warning sign is non-stop, gas-driven ooze that continues after retraction and looks bubbly or unstable.

### The spool lost weight but still prints badly

A spool can lose surface moisture first and still have wet inner wraps. Extend time. If there is still no improvement, check nozzle condition and printer setup.

### The filament was printed wet and parts are weak

Drying the remaining spool can help future prints. It cannot repair parts already printed from wet, hydrolyzed, or foamy material.

For PC, PC/ABS, PC/ASA, nylon, PET, and PBT, hydrolysis during hot processing can reduce mechanical properties. Once the polymer chains have been damaged in the hotend, drying afterward does not undo that printed part damage.

## Compact rules

- A dry purge should be boring.
- Random flow surges, bubbles, popping, and pressure-driven ooze are strong moisture clues.
- Freshly opened filament is not guaranteed to be dry enough for best results.
- Many filament production lines use water cooling before winding.
- A sealed bag and desiccant are storage, not proof of deep drying.
- ABS and ASA are not usually the most moisture-critical FDM materials.
- ABS and ASA still benefit from lower moisture because the process becomes more deterministic.
- CF and GF do not remove the need to dry the base polymer.
- A material name is only a starting point. The exact resin, additives, fillers, colorants, and even color can change drying and printing behavior.
- Check the exact product data sheet instead of assuming that all ABS, ASA, PC-CF, or nylon behaves the same.
- ezPC+CF has an official 80 °C drying recommendation.
- Regular PC-CF may need 95 to 120 °C depending on brand and formulation.
- PA6, PA12, and their CF or GF-filled variants need strict drying and a dry filament path during printing.
- Spool construction can make or break drying.
- The spool hub is often the most restrictive part of the spool.
- If the spool cannot survive the drying temperature, respool first.
- Time, airflow, venting, and true temperature matter more than the dryer label.
- For long prints, dry the spool and print from a dry box.

## References

### Filament drying and symptoms

1. Prusa Knowledge Base, **Drying filament**  
   <https://help.prusa3d.com/article/drying-filament_332086>  
   Used for hygroscopic material notes, moisture symptoms, Prusament drying temperatures, spool temperature limits, dry box notes, and oven warnings.

2. Bambu Lab Wiki, **Filament Drying Recommendations**  
   <https://wiki.bambulab.com/en/filament-acc/filament/dry-filament>  
   Used for the explanation that moisture vaporizes inside the hot nozzle and causes expansion and irregular extrusion.

3. 3DXTech, **Filament Drying Instructions**  
   <https://www.3dxtech.com/pages/filament-drying-instructions>  
   Used for drying temperatures for ABS, ASA, PC, PC/ABS, PC/ASA, nylon, and the note that saturated nylon may need much longer than the starting recommendation.

4. 3DXTech, **CarbonX ezPC+CF**  
   <https://www.3dxtech.com/products/carbonx-ezpc-cf-1>  
   Used for ezPC+CF print range, no heated chamber requirement, and official 80 °C for 4 hours drying recommendation.

### Moisture effects and degradation

5. Toray Plastics, **TOYOLAC ABS/PC PX04 X50 Technical Guide**  
   <https://www.torayplastics.com.my/pdf/toyolac/Technical_guide/PX04_X50_Technical_Guide.pdf>  
   Used for PC type resin drying, hydrolysis, molecular weight decrease, melt viscosity decrease, drooling, gas, silver streaks, and reduced properties.

6. DuPont, **Zytel and Minlon Nylon Resins Molding Guide**  
   <https://dupont.materialdatacenter.com/links/processing/Zytel.pdf>  
   Used for nylon moisture effects, hydrolysis, lower toughness and strength, increased melt flow, lower melt viscosity, splay marks, and internal bubbles.

7. Hamrol, A., Góralski, B., Wichniarek, R., and Kuczko, W., **The Natural Moisture of ABS Filament and Its Influence on the Quality of FFF Products**, Materials, 2023  
   <https://www.mdpi.com/1996-1944/16/3/938>  
   Used for ABS filament moisture behavior and the effect of moisture on tensile strength, dimensional accuracy, and surface structure.

### Manufacturing, new spools, and storage

8. Prusament, **How it is made**  
   <https://prusament.com/how-its-made/>  
   Used for the filament manufacturing process, including pellet dehumidifying and extrusion followed by cooling baths.

9. Labtech Engineering, **High-Speed 3D Filament Extrusion Line**  
   <https://labtechengineering.com/group/high-speed-3d-filament-extrusion-line/>  
   Used as an example of an industrial filament line with a triple chamber water cooling and calibration bath before winding.

10. BOCO Pardubice, **Extrusion line for production of filament**  
    <https://www.boco-extruders.eu/extrusion-line-for-production-of-filament>  
    Used as an example of a filament extrusion line with a cooling tank, drying of the string, haul-off, measurement, and winding.

11. 3DGence, **Is filament drying before use necessary?**  
    <https://3dgence.com/3dnews/is-filament-heating-before-use-necessary/>  
    Used for the caution that tight factory packaging does not guarantee the filament is dry enough to print without preparation, and for the note that material can absorb moisture again during long prints.

### Spools and measurement

12. Hexaxes, **DryAF 100 percent Metal Reusable Spools**  
    <https://hexaxes.com/blogs/blog/dryaf-spools>  
    Used as an example of an open metal spool using aluminium discs, aluminium spacers, high temperature capability, and airflow-focused drying design.

13. FLIR, **How Does Emissivity Affect Thermal Imaging?**  
    <https://www.flir.com/discover/professional-tools/how-does-emissivity-affect-thermal-imaging/>  
    Used for the warning that shiny metal can mislead IR temperature readings and that high-emissivity tape can improve measurement accuracy.

[prusa-drying]: https://help.prusa3d.com/article/drying-filament_332086
[prusament-made]: https://prusament.com/how-its-made/
[3dxtech-drying]: https://www.3dxtech.com/pages/filament-drying-instructions
[3dxtech-ezpc-cf]: https://www.3dxtech.com/products/carbonx-ezpc-cf-1
[bambu-drying]: https://wiki.bambulab.com/en/filament-acc/filament/dry-filament
[toray-abspc]: https://www.torayplastics.com.my/pdf/toyolac/Technical_guide/PX04_X50_Technical_Guide.pdf
[dupont-nylon]: https://dupont.materialdatacenter.com/links/processing/Zytel.pdf
[flir-emissivity]: https://www.flir.com/discover/professional-tools/how-does-emissivity-affect-thermal-imaging/
[hexaxes-dryaf]: https://hexaxes.com/blogs/blog/dryaf-spools
[3dgence-drying]: https://3dgence.com/3dnews/is-filament-heating-before-use-necessary/
[labtech-line]: https://labtechengineering.com/group/high-speed-3d-filament-extrusion-line/
[boco-line]: https://www.boco-extruders.eu/extrusion-line-for-production-of-filament
[hamrol-abs]: https://www.mdpi.com/1996-1944/16/3/938

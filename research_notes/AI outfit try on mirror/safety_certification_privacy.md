# Smart Mirror Electrical Safety, Certification and Privacy Compliance (India primary; US/EU secondary)

> **Research status (16 Oct 2026). Read this first.** This researcher ran six web searches. After that, the web-search budget shared by every agent in this run was used up. The page-fetch tool could not resolve any host, and the egress proxy refused direct downloads (e.g., ftc.gov). As a result:
> 1. Every item under "Cited Findings" comes from search-engine summaries of the linked pages. The pages themselves were not opened, so check exact wording before quoting.
> 2. All other content comes from prior knowledge (training data up to mid-2026). It appears only under **"Gaps → Unverified background"**. Each item has a confidence tag (High/Med/Low) and names the primary document to check.
> 3. **No cost, fee or timeline figure in INR or USD could be sourced.** All such figures are listed as gaps.
> 4. Developments between mid-2026 and Oct 2026 are unverified. Examples: whether the EU "Digital Omnibus" has been adopted, and any change to the DPDP commencement schedule.
>
> A follow-up search pass is needed before publishing exact clause numbers, numeric limits other than the electrical-energy-source limits, or any costs.

---

## 1. Which product-safety standard applies (IEC 62368-1 / Indian adoption) and what it requires in practice

### Takeaway
IEC 62368-1 is the hazard-based safety standard for audio/video and ICT equipment, and it fits a smart mirror (display + AI computer + camera). In India, BIS's Compulsory Registration Scheme (CRS) is moving to **IS/IEC 62368-1:2023**. A MeitY notification of 7 Nov 2025 brought it in to supersede IS 13252 (Part 1):2010 and IS 616:2017, and the old standards may be used concurrently until 1 Nov 2028. In practice the standard requires two things:
- Every part an ordinary person can touch must be a class-1 energy source: ES1 means ≤60 V DC or ≤30 V rms, or touch current ≤2 mA DC or ≤0.5 mA rms. Touch temperatures must stay within the TS1 limits.
- Double or reinforced safeguards must separate mains (ES3) from the user.

### Cited Findings
- **ES1 steady-state limits:** 30 V rms / 42.4 V peak / 60 V DC, with touch current 0.5 mA rms AC, 0.707 mA peak and 2 mA DC. **ES2 limits:** 50 V rms / 70.7 V peak / 120 V DC, with 5 mA rms, 7.07 mA peak and 25 mA DC. A source is ES1 (or ES2) if it does not exceed *either* the voltage limit *or* the current limit for that class. **ES3** exceeds *both* ES2 limits. — [Delta Electronics PSU guide, "SELV, PELV and ES1"](https://psu.deltaww.com/de/industry-know-how/what-is-the-difference-between-selv-pelv-and-es1-in-ac-dc-power-supplies); the classification logic is also given in [EMC.wiki summary](https://www.emc.wiki/thread-5561-1-1.html)
- Ordinary persons may access ES1 under normal operating conditions, and instructed persons may access ES2. Under a single fault condition, the limit is ES2. Element says these limits are in "Table 5" of the standard; table numbering differs between editions. — [Element Materials Technology](https://www.element.com/resources/articles/en-62368-standard-update-information)
- IEC 62368-1 sets limits for touch current and prospective touch voltage for DC, for low-, mid- and high-frequency AC, and for combined AC/DC waveforms. It also sets capacitance and pulse limits. — [UL tech brief "ES vs SELV"](https://japan.ul.com/wp-content/uploads/sites/27/2014/06/1_techbrief_ESvsSELV.pdf)
- **Thermal:**
  - TS1 limits apply to parts an ordinary user can reach.
  - TS2 limits are TS1 + 10 K, and TS3 is anything above TS2.
  - The limits are based on ISO 13732-1:2006.
  - The touch-temperature table is Table 38 in the 2nd edition of IEC 62368-1; earlier text cited by UL calls it Table 42.
  - Sources: [UL tech brief "Touch temperature"](https://japan.ul.com/wp-content/uploads/sites/27/2014/06/1_techbrief_touchtemp.pdf); [Advanced Energy blog](https://www.advancedenergy.com/en-us/about/news/blog/design-considerations-for-maximum-temperature-per-iec-safety-standards/)
- In one interpretation, the ENEC OSM-EE committee applied touch-temperature limits only to the accessible metal bracket of a user-replaceable PC card. In other words, the limits apply to the parts that are accessible once the product is assembled. — [ENEC OSM-EE decision 22/5](https://enec.com/doc/doc_18310_main1_5.3%20OSM%20EE%202022%20decision%2022_5.pdf)
- **India adoption under CRS:**
  - A MeitY notification dated **7 Nov 2025** introduced IS/IEC 62368-1:2023, superseding IS 13252 (Part 1):2010 and IS 616:2017.
  - **Concurrent running** of the old standards is allowed **until 1 Nov 2028**, for both existing and new licences.
  - BIS migration guidelines are dated **9 Mar 2026**.
  - **AR/VR/MR devices** were added as the **65th product category**. Their concurrent window **ended 1 May 2026**, so new licences in that category must use IS/IEC 62368-1:2023.
  - Existing licensees must submit full IS/IEC 62368-1:2023 reports from a BIS-recognised lab for all lead models, plus an undertaking for series models.
  - TVs may also need IS 18112:2025, and phones IS 16333 (Part 3):2022.
  - MeitY's revised series guidelines (**20 May 2026**) allow up to 10 models per series unless a category allows more.
  - These points were attributed jointly across the following search results: [SGS GMA update, Apr 2026](https://www.sgs.com/en-no/news/2026/04/gma-update-april); [Certification-India (MPR)](https://www.certification-india.com/en/updated-bis-standard-for-audio-video-and-ict-equipment-in-india/); [Matrix Test Labs](https://matrixtestlabs.com/blog/meity-announces-migration-to-isiec-62368-12023-a-major-shift-for-electronics-it-product-compliance); [SIQ](https://www.siq.si/?p=35339). The official BIS/MeitY documents were not among the results.
- A licence's R-number stays the same after the standard changes, and labs can already test to the new standard. Grants for new factories or new models are at BIS's discretion, so timing is uncertain. — [Nemko blog (Chinese)](https://www.nemko.com/zh-hant/blog/%E5%8D%B0%E5%BA%A6bis%E8%AA%8D%E8%AD%89%E6%9B%B4%E6%96%B0)

### Inferences
- **Energy sources in the mirror:**
  - The mains inlet and the PSU primary are ES3, and the primary is PS3.
  - Rails at 5, 12 and 24 V DC are all below the 60 V DC ES1 voltage limit.
  - Because classification uses "voltage *or* current", a 24 V rail is ES1 whatever its current. That only holds if it stays ES1 under single-fault conditions, which requires reinforced or double insulation inside the PSU.
  - Once all reachable circuits are ES1, the main hazards left on the secondary side are **fire (power source class)**, **heat (TS)**, **mechanical** (glass, mass, tip-over) and **optical radiation**. Shock is no longer one of them.
- **Edition to design to:** new categories already have to use IS/IEC 62368-1:2023, and all categories must migrate by 1 Nov 2028. A new product should therefore be designed and tested directly to the current IEC 62368-1 edition rather than to IS 13252 (Part 1):2010. That avoids re-testing within the product's life.
- **Legal vs good practice:** conforming to IEC 62368-1 (or its national version) is a **legal requirement** only where a regulation calls it up. That covers India CRS for listed categories (see Q5) and the EU, where it is the presumption-of-conformity route under RED/LVD. In the US it is a de facto market requirement (see Q6). Following it for a product outside those regimes is still the best available evidence of safety for product-liability purposes.

### Gaps
- None of the standard's text could be read, so clause numbers and numeric tables other than the ES limits are unverified. This includes the TS1 values, touch-current measurement, Class I/II rules, the tool-access rule, fusing and cord anchorage.
- **Unverified background (prior knowledge; check against the IEC 62368-1:2018/2023 text):**
  - [High] **Hazard-based structure.** The standard classifies energy sources and then places safeguards (basic, supplementary, reinforced, plus "instructional" safeguards) between class-2/3 sources and body parts.
    - Electrical: ES1–ES3.
    - Power/fire: PS1–PS3.
    - Mechanical: MS1–MS3.
    - Thermal: TS1–TS3.
    - Radiation: RS1–RS3.
  - [High] **Safeguards required for ordinary persons:** none for ES1; a basic safeguard for ES2; basic + supplementary (double) or reinforced for ES3.
  - [High] **ES1 definition (cl. 5.2.1.1):**
    - It must stay within ES1 limits under normal and abnormal operating conditions, and under single faults of components that are not safeguards.
    - It must stay within ES2 limits under a single fault of a basic or supplementary safeguard.
    - This is why the PSU's mains-to-output insulation must be reinforced or double.
  - [Med] **Class I** (protective earthing) vs **Class II** (double/reinforced insulation):
    - Cl. 5.6 covers protective conductors, bonding and the bonding-resistance test.
    - Cl. 5.7 covers touch current and protective-conductor current, measured with IEC 60990 networks.
    - Cl. 5.7.6 adds requirements where touch current exceeds ES2 limits: protective-earth conductor requirements and a "high touch current — earth before connecting supply" warning.
    - Check the exact limits for Class I pluggable type A equipment.
  - [Med-High] **TS1 limit for long contact:** 43 °C applies to surfaces touched continuously for more than 8 h, whatever the material (ISO 13732-1 basis). Short-contact limits are higher, and higher for glass/plastic than for metal (Table 38). A sensible design target is **≤43 °C on the front glass** at maximum rated ambient.
  - [High] **Accessibility and tool access:** accessibility is judged with the Annex V probes (e.g., the jointed test finger). Covers that can be removed without a tool are taken off for the test. Mains parts must therefore sit behind fixings that need a tool.
  - [High] **Power-source classes:** PS1 ≤15 W, PS2 ≤100 W, PS3 >100 W. PS3 circuits need a fire enclosure.
  - [Med] **Annex Q limited power source:** for ≤30 V outputs the limits are ≤8 A and ≤100 VA.
  - [Med] Annex G.7 covers mains supply cords: cord anchorage/strain relief with pull and torque tests, and bend protection. Annex G.3 covers protective devices such as fuses and thermal cut-offs. Check the force and torque values.
  - [Med] **Mechanical clauses:**
    - Cl. 8.6 covers stability (tilt and horizontal-force tests).
    - Cl. 8.7 covers equipment mounted on a wall, ceiling or other structure (a downward-force test at a multiple of the equipment's weight).
    - Glass is covered by cl. 4.4.3.6 (glass impact) and Annex T.9.
    - Mass classes are roughly MS1 ≤7 kg, MS2 ≤25 kg and MS3 >25 kg. Check all numbers.
  - [High] **Optical radiation:** emissions from LEDs, including the IR LEDs in IR touch frames and camera illuminators, are assessed under cl. 10 using IEC 62471 risk groups.
  - [Med-High] **Coin/button cells:** cl. 4.8 (2018 edition onwards) requires a battery compartment that needs a tool or two independent movements to open, plus tests and warnings.
  - [High] **Earlier Indian standards:** IS 13252 (Part 1):2010 was India's adoption of IEC 60950-1, not of IEC 62368-1. IS 616:2017 adopted IEC 60065.
  - [Med] **Editions and the CB Scheme:**
    - IEC 62368-1 editions: 2nd (2014), 3rd (2018), 4th (2023). Check which IEC edition IS/IEC 62368-1:2023 is identical to.
    - The IECEE CB Scheme lets one CB report support EU and US NRTL approvals.
    - BIS CRS requires testing in a BIS-recognised lab and does not accept CB reports in lieu.

---

## 2. Practical design rules: users must never contact hazardous voltage

### Takeaway
The robust architecture has five parts:
- Confine mains to a single certified power supply in a sealed, tool-access-only compartment, or use an external Class II adaptor.
- Run everything a user can reach on ES1 DC (5/12/24 V), split into current-limited branches of ≤100 W.
- Sense touch *through* the glass, so users only ever touch glass and the frame.
- Use Class II construction, so safety never depends on the household earth.
- Keep the front glass at or below about 43 °C.

These are good practice rather than law. They are the easiest way to meet the legally referenced standard (Q1).

### Cited Findings
- Common DC rails (5/12/24 V) are below the ES1 DC limit of 60 V. A source is ES1 if it is within either the voltage limit or the current limit. — [Delta Electronics PSU guide](https://psu.deltaww.com/de/industry-know-how/what-is-the-difference-between-selv-pelv-and-es1-in-ac-dc-power-supplies)
- ES1 accessible-part touch-current limits are 0.5 mA rms AC and 2 mA DC. — [Delta Electronics PSU guide](https://psu.deltaww.com/de/industry-know-how/what-is-the-difference-between-selv-pelv-and-es1-in-ac-dc-power-supplies)
- Power adapters are listed CRS product categories in India. — [Seyecs CRS guide 2026](https://blogs.seyecs.com/bis-certification-for-electronic-products/); [eChai CRS page](https://echai.ventures/d2c/d2c-product-licenses/bis-crs-mark-electronics)

### Inferences
These design rules are this researcher's synthesis. "[Legal driver]" means the rule directly serves a mandatory requirement; "[Good practice]" means it does not.

1. **Mains boundary** [Good practice → makes the 62368-1 safeguards easy]. Put the only ES3/PS3 part in a pre-certified PSU. There are two options:
   - **(a) External Class II desktop adaptor.** This is simplest: the mirror itself becomes an ES1-only product. In India the adaptor needs its own CRS registration, since adapters are a listed category.
   - **(b) Internal certified PSU** in a sealed sub-enclosure that only a tool can open. The sub-enclosure should be metal or flame-rated V-0 plastic and include:
     - an IEC 60320 appliance inlet;
     - a line fuse;
     - cord anchorage or strain relief;
     - a mains-warning label on the cover.

   Option (a) also keeps mains outside a product that people lean on and clean daily.
2. **Low-voltage distribution** [Good practice; fire safety].
   - Feed every user-reachable function from ≤24 V DC: LED lighting, the display's logic board, the camera, the AI computer, the touch frame, speakers and sensors.
   - Avoid 230 V AC LED strips and mains-voltage lighting entirely.
   - Split the DC bus into branches of ≤100 W each with current limiting (eFuse/PTC), so each branch is a PS2 or limited-power circuit. This minimises fire-enclosure needs on the secondary side; check against 62368-1 cl. 6 and Annex Q.
3. **Touch only glass** [Good practice].
   - Use an **IR touch frame** (an LED/photodiode bezel around the glass) or a **projected-capacitive (PCAP) foil** bonded to the rear of the glass.
   - Users then touch glass, an insulator, and never an electrode or conductor.
   - Route ESD that arrives at the bezel or frame to circuit ground through TVS diodes and a defined chassis bond.
4. **Earthing** [Legal driver if Class I].
   - **Prefer Class II for India**, because household earthing cannot be assumed (see Q3).
   - If a Class I (3-pin, earthed) inlet is used, bond every accessible metal part to protective earth with a dedicated conductor and pass the bonding test. Examples: an aluminium frame, the back panel, the VESA bracket.
5. **Touch current across the isolation barrier** [Legal driver].
   - Class II switch-mode PSUs usually have EMI capacitors across the isolation barrier. Their leakage to touchable secondary parts must stay within the ES1 touch-current limit of 0.5 mA rms.
   - When several supplies feed one product, their leakages add, so measure the whole product, not each PSU alone.
6. **Thermal** [Legal driver: TS1].
   - Keep the hot parts away from the rear of the glass and use chimney ventilation; the hot parts are the AI computer, the LED drivers and the display backlight.
   - Add temperature sensing with throttling and shutdown.
   - Verify ≤43 °C on the front glass at the highest rated ambient temperature. Indian rooms in summer can be hot, so rate the ambient conservatively.
7. **Liquids** [Good practice].
   - Users spray glass cleaner on mirrors daily. Provide a sealed bottom edge and drip path, and keep electronics above the lower edge.
   - Gasket the touch frame.
   - If bathroom use is allowed, design for IPX4 (see Q3).
8. **Servicing** [Good practice]. Make no parts user-serviceable, use security or tool-only fasteners on every compartment, and put an internal warning label on the PSU compartment.
9. **Cells** [Legal driver: 62368-1 cl. 4.8; US Reese's Law — see Q8]. Do not use user-accessible coin cells. An RTC cell, if fitted, belongs inside the tool-access compartment.
10. **Camera hardware privacy controls**: see Q7. Two of them double as safety and privacy features: a hardware camera power switch and an LED wired to the sensor's supply.

### Gaps
- No sources were retrieved on any of the following:
  - IR-frame vs PCAP performance through mirror glass;
  - ESD test levels;
  - the conductivity of semi-transparent mirror coatings.
- **Unverified background (prior knowledge):**
  - [Med] **ESD immunity** is tested per IEC 61000-4-2 within the EMC immunity standard CISPR 35 / EN 55035. Typical levels are ±4 kV contact and ±8 kV air; check the edition's levels. Many touch-product makers design to higher margins.
  - [Med] **Mirror coatings and PCAP.** Some semi-transparent ("two-way") mirror coatings are metallic and therefore conductive. They can block PCAP sensing, and must be kept isolated from circuits or deliberately bonded. Dielectric (non-metallic) beam-splitter coatings or IR frames avoid this. Confirm with the glass supplier.
  - [High] **SELV vs ES1.** SELV (from the older IEC 60950-1/IEC 61140 framework) is broadly comparable to ES1 for the purpose of designing low-voltage circuits. The Delta article compares SELV, PELV and ES1, but its detailed content was not read.

---

## 3. Household protection in India: RCD/RCCB, surge protection and bathroom installation

### Takeaway
This session could not retrieve the text of the CEA (Measures relating to Safety and Electric Supply) Regulations 2023, IS 732 or the National Electrical Code 2023. What the general sources confirm is that 30 mA RCDs give "additional" protection against electrocution, because the other protective measures are not infallible. The product should therefore not *depend* on a household RCD or a good earth; that means Class II/ES1 design. Recommending a 30 mA RCCB-protected socket, surge protection and bathroom limits is good practice for the user manual and installation guide.

### Cited Findings
- High-sensitivity RCDs (IΔn ≤ 30 mA) disconnect the supply automatically to prevent injury or death by electrocution. They are described as "additional" protection because the preceding protective measures "cannot be regarded as being infallible". — [Schneider Electric technical guide](https://download.schneider-electric.com/doc/CA908066E/CA908066E%20%28web%29.pdf)
- A manufacturer's installation guide says its leakage-current device trips within a maximum of 30 ms on a fault, and advises testing the device at least monthly. — [Gira installation guide](https://download.gira.com/data3/01141190.pdf)
- Residential 30 mA Type A RCCBs are certified to EN/IEC 61008. — [RS Online, Schneider Resi9 XE RCCB listing](https://ie.rs-online.com/web/p/rccbs/2768941)
- The search for the CEA Safety Regulations 2023 clause on earth-leakage protection returned no copy of the regulation. Its requirement could not be confirmed in this session. — (search returned only product pages; see the Schneider and Gira links above)

### Inferences
- **Do not rely on site protection** [Good practice]. Earthing quality and RCD presence vary from home to home, so a Class II, ES1-only product stays safe even on a socket with no earth and no RCD.
- **Manual and installation guidance** [Good practice; consumer-protection duty to warn]:
  - Recommend a socket on a 30 mA RCCB-protected circuit (IEC 61008 / Indian equivalent).
  - Tell users to press the RCCB test button monthly, as manufacturers advise.
  - Recommend a plug-in surge protector, or a surge protective device at the distribution board.
  - Specify the minimum wall type and anchors (see Q4).
- **Bathrooms.** Either:
  - (a) state that the product is "not for bathrooms or wet locations" and design for indoor dry use; or
  - (b) design an IPX4 (ideally IP44) variant and specify where it may be installed relative to the bath or shower, connected by an electrician to an RCD-protected circuit.

  Option (a) is far cheaper for a first product.
- **Supply quality** [Good practice]. Use a universal or wide-input PSU with surge and over-voltage robustness, because Indian supply voltage can swing and spike (prior knowledge; see Gaps).

### Gaps
- **Unverified background (prior knowledge; check the official texts):**
  - [Med] **CEA Regulations.**
    - Regulation 42 of the CEA (Measures relating to Safety and Electric Supply) Regulations, **2010**, required an earth-leakage protective device that disconnects the supply on an earth fault or leakage. It applied to installations other than those at ≤250 V with load below 5 kW, i.e., roughly installations above 5 kW.
    - The **2023** Regulations superseded the 2010 ones and keep an equivalent earth-leakage requirement. Check the 2023 regulation number, the kW threshold and whether 30 mA is specified (Gazette text on cea.nic.in).
  - [Med] **IS 732:2019** (Code of practice for electrical wiring installations) is aligned with IEC 60364. It calls for additional protection by RCDs of ≤30 mA on general-use socket outlets up to 32 A, mirroring IEC 60364-4-41 cl. 411.3.3. Check the clause.
  - [Med] **National Electrical Code of India 2023 (BIS SP 30:2023)** has residential recommendations including RCDs and rules for locations containing a bath or shower. Check the sections.
  - [Med-High] **IEC 60364-7-701 (bath/shower locations)**:
    - It defines zones 0, 1 and 2 around the bath or shower.
    - Equipment in zones 1 and 2 needs at least IPX4 (IPX5 where water jets are used for cleaning).
    - All circuits serving the location need ≤30 mA RCD protection.
    - SELV at ≤12 V AC or ≤30 V DC is permitted in the inner zones, with the source outside them.
    - Socket outlets are restricted near the zones.
    - Check the zone dimensions and the edition (2019).
  - [High] **IEC 60529:** IP44 means protection against solid objects ≥1 mm and against splashing water from any direction.
  - [Med] **Surge immunity:** the product's AC mains port is surge-tested per IEC 61000-4-5 within CISPR 35/EN 55035 (typically ±1 kV line-to-line and ±2 kV line-to-earth; check). Household SPDs follow IEC 61643-11.
  - [Low] Indian statutory limits on supply-voltage variation (historically ±6% at LV under the Indian Electricity Rules 1956, Rule 54) — current CEA limit unverified.

---

## 4. Mechanical safety: glass type, anti-shatter film, weight, wall anchoring and anti-tip

### Takeaway
No sources on glass or anchoring standards could be retrieved in this session. From prior knowledge, a large vertical mirror that is not continuously backed should use safety glazing, and a mirror with a display behind it is not continuously backed. The safety glazing should be **laminated** glass, which holds its fragments when broken, or **tempered glass with an optically clear safety film**. Its impact class should be verified (EN 12600 / ANSI Z97.1 / IS 2553). Wall anchoring and an anti-tip restraint should be treated as non-negotiable design features. IEC 62368-1's stability (cl. 8.6) and wall-mount (cl. 8.7) tests apply to the product itself. Furniture tip-over laws such as the US STURDY Act legally cover clothing-storage units, not mirrors, but they are good benchmarks.

### Cited Findings
- No findings could be retrieved: the web-search budget was exhausted and page fetching was unavailable. See Gaps.

### Inferences
- **Weight drives anchoring.** Using the standard density of float glass (about 2.5 kg/m² per mm of thickness; prior knowledge), the weights work out as follows:
  - 6 mm glass weighs about 15 kg/m².
  - A full-length 1.8 m × 0.6 m mirror therefore carries about 16 kg of glass alone.
  - Adding a large display panel, the compute module, the frame and the touch bezel brings the total plausibly to **25–40 kg**.

  At that weight a fall is a crushing and laceration hazard, so mounting must be load-tested with margin. 62368-1 cl. 8.7 uses a multiple of the product weight (check the value).
- **Glass choice** [Good practice; possibly legal in building-code jurisdictions]:
  - **Laminated:** two plies with a PVB/EVA interlayer, with the mirror coating protected inside. When it breaks, the pieces stay attached.
  - **Tempered:** breaks into small dice, but large panels can still release a cascade of fragments. Rare spontaneous breakage is possible unless the glass is heat-soaked.
  - **For a touch-and-lean surface at body height, laminated is the safer default.** If tempered glass is used, add a full-coverage, optically clear safety film on the rear.
- **Floor-standing (leaning or cheval) designs** [Good practice]. A heavy panel can tip when a child pulls on it or climbs it. The design should include:
  - a supplied wall-anchor strap;
  - a wide base;
  - a low centre of gravity, with compute and PSU mounted low;
  - a test equivalent to the 62368-1 tilt and horizontal-force tests, using ASTM F2057-23-style child-climb loading as a stretch benchmark.
- **Wall-mounted designs** [Good practice]. Supply a French cleat or Z-bracket and anchors suited to the wall type: masonry or RCC fasteners for typical Indian walls, studs for drywall. Specify professional installation for units above a weight threshold.

### Gaps
- **Unverified background (prior knowledge):**
  - [High] **Glass standards:**
    - Tempered (toughened) glass: EN 12150-1. Heat-soak testing to reduce nickel-sulphide spontaneous breakage: EN 14179-1.
    - Laminated safety glass: EN ISO 12543 / EN 14449.
    - Pendulum impact classification: EN 12600 (classes 1/2/3, class 1 being the most severe drop height).
  - [High] **US glazing rules:**
    - CPSC 16 CFR 1201 is the safety standard for architectural glazing (doors, shower/bath enclosures, etc.), with Category I/II impact levels.
    - ANSI Z97.1 is the voluntary safety-glazing standard.
    - [Med] The IBC/IRC hazardous-location glazing rules (IBC 2406.4 / IRC R308.4) exempt mirrors mounted on a surface that provides continuous backing support. A display mirror has no continuous backing, so the exemption would not apply.
  - [Med] **India glass:** IS 2553 (Part 1) covers safety glass. The National Building Code 2016, Part 6 Sec. 8 ("Glass and Glazing"), covers human-impact safety. Check whether either applies to a free-standing or wall-hung product rather than to building glazing.
  - [High] **US tip-over law:** the STURDY Act (Dec 2022) made **ASTM F2057-23** the mandatory federal standard for clothing-storage units from 1 Sep 2023. Its scope does not include mirrors. The CPSC's "Anchor It!" campaign covers TVs and furniture.
  - [Med] **EU:**
    - The General Product Safety Regulation (EU) 2023/988 requires overall safety.
    - EN 14749 (domestic storage units) and EN 14072 (glass in furniture) are usable benchmarks.
    - No harmonised "smart mirror" mechanical standard is known to this researcher.
  - [Low] India also has furniture Quality Control Orders (QCOs). One search summary said furniture and household-appliance QCOs were phasing in through 2026 and that ~20 QCOs, mostly chemicals and metals, were revoked in late 2025. The source page for this could not be identified, so check applicability to a mirror product.

---

## 5. Certification in India: BIS CRS, WPC ETA, TEC MTCTE, e-waste EPR

### Takeaway
CRS (MeitY's Electronics and IT Goods compulsory-registration Order, 2021) covers a fixed list of categories. Vendor guides count about 74 to 75+ categories, while the migration notices call AR/VR/MR the "65th". **"Smart mirror" is not a named category in any source found.** CRS therefore applies with certainty to the mirror's listed **sub-components** (power adaptor, LED lighting, and Li-ion cells if used). Whether it applies to the **whole product** depends on BIS/MeitY classifying it under a listed category such as a display or monitor, so get a written category determination. New registrations should be tested to IS/IEC 62368-1:2023. WPC Equipment Type Approval (Wi-Fi/Bluetooth), possible MTCTE, and e-waste EPR registration also apply, but their details and **all fees and timelines could not be verified** this session.

### Cited Findings
- **Category count:** CRS covers roughly 74 electronics/IT categories in one guide and "75+" in a 2026 guide. Another list counts 81 items across five ministries, apparently mixing CRS with other QCOs. The counts are inconsistent. — [Seyecs CRS guide 2026](https://blogs.seyecs.com/bis-certification-for-electronic-products/); [ChemRadar inventory wiki](https://www.chemradar.com/inventory-wiki/cupdvh2wgmww)
- **Example covered categories:**
  - IT and displays: laptops, desktops, monitors, printers, scanners, visual display units (VDUs).
  - Also: mobile phones, LED lights, power adapters, "smart devices".
  - Separately: power banks, smart watches and solar items under "Scheme II".
  - Sources: [Seyecs](https://blogs.seyecs.com/bis-certification-for-electronic-products/); [eChai](https://echai.ventures/d2c/d2c-product-licenses/bis-crs-mark-electronics); [PSR Compliance](https://www.psrcompliance.com/bis-crs-registration)
- BIS guidance placed audio glasses, smart glasses, AR glasses and MR glasses under the 2021 Electronics and IT Goods Order, with **separate BIS registration required per product category**. — [CliniExperts regulatory update](https://cliniexperts.com/regulatory-update/guidance-on-product-category-under-compulsory-registration-scheme-crs/)
- Laptops, notebooks and tablets are moving from IS 13252 (Part 1):2010 to IS/IEC 62368-1:2023, with a concurrent-running deadline of 1 Nov 2028. — [Seyecs laptop/tablet guide](https://blogs.seyecs.com/bis-crs-registration-for-laptop-notebook-tablet/)
- **Licence validity (sources conflict):** one 2026 guide says CRS (Scheme-II) licences are valid for **five years as of 25 Feb 2026**, while another guide in the same results says about two years. — [AgileRegulatory 2026 update](https://www.agileregulatory.com/blogs/bis-crs-registration-2026-revised-testing-labeling-and-documentation-rules); the conflicting guide could not be attributed precisely.
- The migration notes and series rules from Q1 also apply here: IS/IEC 62368-1:2023, 1 Nov 2028, and up to 10 models per series from 20 May 2026. — [SGS GMA update Apr 2026](https://www.sgs.com/en-no/news/2026/04/gma-update-april); [Matrix Test Labs](https://matrixtestlabs.com/blog/meity-announces-migration-to-isiec-62368-12023-a-major-shift-for-electronics-it-product-compliance)
- A TÜV SÜD 2025 GMA newsletter has an India wireless article. Only its title was seen, so its contents are unknown. — [TÜV SÜD GMA newsletter 2025, "Wireless India"](https://www.tuvsud.com/zh-tw/services/global-market-access/gma-newsletter-2025/tw-articles/12-wireless-india)

### Inferences
- **Does a smart mirror fall under CRS?** Probably not as a named category. CRS is category-based: categories such as AR/MR glasses needed explicit guidance and their own registration, which shows that an unlisted product type is not automatically in scope. The risks and requirements are:
  - (i) A large integrated display could be treated as a "monitor/VDU"-type product. Check the size thresholds in the Order.
  - (ii) Listed sub-assemblies must carry their own CRS registration in any case: the power adapter, LED lighting and any lithium cells.
  - (iii) The safest path is to write to MeitY/BIS for a product-category clarification before launch.
- **Choose CRS-registered parts.** Using CRS-registered adaptors, LED drivers and battery packs cuts India time-to-market even if the whole product turns out to be outside CRS.
- **Legal requirements vs good practice in India:**

| Item | Status | Note |
|---|---|---|
| CRS registration of listed components (adaptor, LED lighting, Li-ion cells/batteries) | **Legal** (where the component is a listed category) | Sourced: adapters, LED lights and power banks are listed |
| CRS for the whole mirror | **Legal only if classified into a listed category** | Get a written determination |
| WPC ETA for Wi-Fi/BT | **Legal** (prior knowledge; see Gaps) | Even with a pre-approved module, check whether the host needs its own ETA |
| TEC MTCTE | **Legal only if a notified telecom category applies** | Check categories such as smart camera, IoT gateway, Wi-Fi CPE |
| E-waste EPR registration (CPCB) | **Legal** (prior knowledge) | Must be in place before sale |
| Battery Waste Management Rules EPR | **Legal if a battery is included** (prior knowledge) | |
| Testing to IS/IEC 62368-1:2023 now rather than IS 13252:2010 | Good practice | Avoids re-testing before 2028 |
| Written category ruling from BIS/MeitY | Good practice | Reduces enforcement and customs risk |

### Gaps
- **Costs and timelines (INR):** no BIS CRS fees, lab test charges, ETA or MTCTE fees, CPCB EPR fees or typical durations could be sourced. They need a follow-up search of crsbis.in, saralsanchar.gov.in, mtcte.tec.gov.in and eprewastecpcb.in, plus quotes from BIS-recognised labs.
- **Unverified background (prior knowledge):**
  - [High] **Legal basis of CRS:**
    - The Order is the "Electronics and Information Technology Goods (Requirements for Compulsory Registration) Order, 2021", issued under the BIS Act 2016. Check the exact title wording.
    - Registration is under Scheme-II of Schedule II of the BIS (Conformity Assessment) Regulations, 2018.
    - Testing must be done only in BIS-recognised labs.
    - Foreign manufacturers need an Authorised Indian Representative.
    - Products carry the Standard Mark with an R-number.
  - [Med] **32-inch thresholds:** the TV and video-monitor categories have historically carried a "32 inches and above" screen-size threshold. Check the current wording, because it bears on whether a mirror with a large display could be classified as a monitor.
  - [Med] **CCTV:** MeitY's "Essential Requirements for Security of CCTV" (with STQC testing) became mandatory for CCTV cameras under CRS from about April 2025. A mirror with a camera is not a CCTV camera unless it is marketed for surveillance or remote viewing. Avoid security-camera positioning.
  - [High/Low] **WPC ETA:** Equipment Type Approval is required before importing or selling wireless equipment, including Wi-Fi and Bluetooth [High]. For products using de-licensed bands, a **self-declaration** route exists on the Saral Sanchar portal, backed by an RF test report from an accredited lab [High]. The fee and processing time are unverified [Low].
  - [Med] **MTCTE:** TEC's Mandatory Testing and Certification of Telecommunication Equipment applies only to notified equipment categories, introduced in phases. Check on mtcte.tec.gov.in whether any IoT, camera or Wi-Fi-device category captures the product.
  - [High/Med] **E-waste and battery EPR:**
    - The E-Waste (Management) Rules 2022 took effect on 1 Apr 2023. Producers of electrical and electronic equipment listed in Schedule I must register on CPCB's EPR portal and meet recycling targets through EPR certificates [High].
    - A floor price for EPR certificates was introduced by a later amendment and has been challenged in court by manufacturers [Med]. Check the amount and the current status.
    - The Battery Waste Management Rules 2022 impose EPR where batteries are included [High].
    - Plastic-packaging EPR applies to brand owners [High].
  - [High] **Labelling:** the Legal Metrology (Packaged Commodities) Rules 2011 require package labelling such as MRP, manufacturer/importer details and net quantity.
  - [High] **CERT-In Directions:** the CERT-In Directions of 28 Apr 2022 (IT Act s.70B) require reporting cyber incidents within 6 hours and keeping ICT logs for 180 days in India. They apply to the company's cloud and app backend.
  - [High] **Product liability:** the Consumer Protection Act 2019 has product-liability provisions (Chapter VI) that make the manufacturer liable for harm from defective products. A safety-standard test report is the main defence evidence.
  - [Low] **Machinery/electrical OTR:** the status of the Machinery and Electrical Equipment Safety (Omnibus Technical Regulation) Order 2024 is unknown. It was announced for low-voltage electrical equipment and reportedly deferred. Check whether it could capture products not covered by CRS.

---

## 6. Certification in the US and EU: FCC, UL/NRTL, CE marking

### Takeaway
No US/EU sources could be retrieved in this session. From prior knowledge:
- **US:** the digital device needs an FCC Part 15 Subpart B **Supplier's Declaration of Conformity (SDoC)**. Wi-Fi/BT radios need **Certification** (FCC ID), or a modular-approved module can be reused under 47 CFR 15.212. UL 62368-1 **NRTL listing** is not federally required for consumer sales, but retailers, insurers and building inspectors expect it.
- **EU:** CE marking falls under the **Radio Equipment Directive**, which absorbs the LVD safety and EMC objectives for radio products. RED cybersecurity requirements are mandatory from 1 Aug 2025. RoHS, WEEE, GPSR, possibly the Ecodesign rules for electronic displays and standby, and the **Cyber Resilience Act** also apply; CRA vulnerability reporting applies from 11 Sep 2026.
- All costs and timelines are unverified.

### Cited Findings
- No findings could be retrieved: the web-search budget was exhausted and page fetching was unavailable. See Gaps.

### Inferences
- **One test campaign for all markets** [Good practice]. Test to IEC 62368-1 (CB report) plus CISPR 32/35 EMC plus radio standards, and reuse the results for EU self-declaration and the US NRTL listing. India still needs testing in a BIS-recognised lab (Q5).
- **Use pre-certified radio modules** that already hold FCC modular approval, RED evidence and India ETA. This is the biggest single cost and time saver; see Gaps for why.
- **Legal requirements vs good practice (US/EU):**

| Market | Legal requirement | Good practice / market expectation |
|---|---|---|
| US | FCC Part 15 (SDoC for the digital device; Certification or modular reuse for radios); FCC Covered List restrictions; FTC Act §5 (truthful privacy/security claims); COPPA if children under 13; state biometric/privacy laws; CPSC defect reporting; Reese's Law if button/coin cells | NRTL listing to UL 62368-1; US Cyber Trust Mark; ETSI EN 303 645 / NISTIR 8259A security baseline |
| EU | CE marking under RED 2014/53/EU (Art. 3(1)(a) safety, 3(1)(b) EMC, 3(2) radio, 3(3)(d)(e)(f) cybersecurity); RoHS; WEEE registration in each member state sold into; GPSR; EU economic operator (MSR Art. 4); Ecodesign display/standby rules if in scope; Battery Regulation if battery; CRA reporting (from 11 Sep 2026) and full CRA (11 Dec 2027); GDPR; AI Act | EN 18031 series applied in full; ETSI EN 303 645 |

### Gaps
- **Costs and timelines (USD/EUR) for FCC SDoC/certification, NRTL listing and CE test campaigns are not sourced.** Get quotes from UL Solutions, Intertek, TÜV SÜD, TÜV Rheinland and SGS.
- **Unverified background (prior knowledge):**
  - [High] **FCC authorisation routes:**
    - 47 CFR Part 15 Subpart B Class B (residential) limits apply to the digital device, authorised by **SDoC** (47 CFR 2.906; SDoC replaced Verification/DoC in 2017).
    - Intentional radiators need **Certification** through a Telecommunication Certification Body, with an FCC ID (47 CFR 2.907; Part 15 Subpart C §15.247 / Subpart E §15.407 for Wi-Fi).
    - Under **modular approval** (§15.212), the host carries a "Contains FCC ID" label plus an SDoC for Subpart B.
  - [High] **Covered List:**
    - The FCC Covered List (Nov 2022 order) bars equipment authorisation for equipment from Huawei, ZTE, Hytera, Hikvision and Dahua. Avoid their camera and radio modules.
    - [Med] In 2025 the FCC moved to bar test labs and certification bodies controlled by "foreign adversaries", and to restrict covered-entity modular transmitters. Check the status.
  - [High/Low] **US Cyber Trust Mark:** the voluntary IoT security label launched in Jan 2025 [High]. Its administration was under FCC scrutiny in 2025, so check its current status [Low].
  - [High] **NRTL listing:** OSHA requires NRTL-listed equipment in **workplaces** (29 CFR 1910.303, 1910.399). There is **no federal NRTL mandate for consumer sales**, but major retailers, insurers and electrical inspectors expect it under the NEC "listed" provisions.
  - [Med-High] **Legacy standards withdrawn:** UL 60950-1 and UL 60065 were withdrawn in favour of UL 62368-1 around Dec 2020. EN 62368-1 likewise replaced EN 60950-1/EN 60065 as the harmonised EU standard.
  - [High] **Reese's Law:** CPSC rule 16 CFR 1263 (Reese's Law; effective 19 Mar 2024) requires secured battery compartments and warnings on consumer products containing button or coin cells.
  - [High] **RED covers safety and EMC.** For radio equipment, RED Art. 3(1)(a) covers safety with the LVD objectives but no lower voltage limit, and Art. 3(1)(b) covers EMC. LVD 2014/35/EU and EMC 2014/30/EU therefore do not apply separately.
  - [High] **RED cybersecurity:** Delegated Regulation (EU) 2022/30 (cybersecurity, privacy and anti-fraud) has been mandatory since **1 Aug 2025**. The harmonised standards are EN 18031-1/-2/-3:2024 [Med: cited in the OJ in Jan 2025 with restrictions]. Where a restriction applies, for example allowing users to skip setting a password, a notified body becomes necessary [Med].
  - [High] **RoHS:** RoHS 2011/65/EU as amended by (EU) 2015/863 restricts 10 substances.
  - [High] **WEEE:** under WEEE 2012/19/EU, the producer registers in each member state and the product carries the crossed-out-bin symbol.
  - [High] **GPSR and EU operator:** GPSR (EU) 2023/988 has applied since **13 Dec 2024**. Market Surveillance Regulation (EU) 2019/1020 Art. 4 requires an EU-based economic operator for CE-marked products.
  - [High/Med] **Ecodesign and energy labelling:**
    - The Ecodesign regulation for electronic displays (EU) 2019/2021 and the energy-label regulation (EU) 2019/2013 apply from 1 Mar 2021 to displays over 100 cm² [High]. **Whether a smart mirror counts as an "electronic display" needs a determination** [Med].
    - Networked-standby ecodesign (EU) 2023/826 applies from 9 May 2025 [Med-High].
  - [High] **Cyber Resilience Act (EU) 2024/2847:**
    - Art. 14 reporting of actively exploited vulnerabilities and severe incidents applies from **11 Sep 2026**, i.e., *already in force* as of Oct 2026.
    - Full obligations apply from **11 Dec 2027**.
    - [Med] Annex III Class I lists "smart home products with security functionalities", including **security cameras**. Avoid positioning the mirror as a security camera.
  - [High] **Battery Regulation (EU) 2023/1542:** portable batteries in appliances must be **removable and replaceable by the end user from 18 Feb 2027** (Art. 11).
  - [Low] **UK:** if the UK is ever targeted, the PSTI Act 2022 product-security regime has been in force since 29 Apr 2024 (no default passwords, vulnerability-disclosure policy, stated support period).

---

## 7. Privacy: a camera in a bedroom or dressing area (India DPDP; EU GDPR/AI Act; US FTC)

### Takeaway
India's **DPDP Rules 2025 were notified on 13 Nov 2025** (Gazette G.S.R. 846(E) per secondary sources) and commence in phases:
- Data Protection Board provisions applied immediately.
- **Consent-manager provisions apply after about 12 months (around 13/14 Nov 2026, i.e., next month).**
- **Most obligations of data fiduciaries apply after 18 months (around 13/14 May 2027).** These cover notice, consent, security safeguards, 72-hour breach reporting, data-principal rights and children's verifiable parental consent.

A product launching in 2026–27 should therefore comply from day one. For a camera in a space where people change clothes, the defensible design has these elements:
- on-device processing, with no image upload by default;
- a physical shutter;
- a hardware-wired indicator LED;
- no human review of images;
- explicit consent;
- easy deletion.

Enforcement history in the US (e.g., Ring 2023) shows the cost of failing at this. Those incident details are unverified this session.

### Cited Findings
- The Government of India notified the DPDP Rules, 2025, "marking the full operationalisation of the DPDP Act, 2023". The notification date was **13 Nov 2025**. — [PIB press release](https://www.pib.gov.in/PressReleasePage.aspx?PRID=2190014&reg=3&lang=2)
- **Phased start:**
  - Data Protection Board provisions take effect immediately.
  - Consent-manager provisions apply after 12 months.
  - Most data-fiduciary obligations apply after 18 months (May 2027), covering notices, consent, security safeguards, breach reporting and data-principal rights.
  - Sources: [EY India](https://www.ey.com/en_in/insights/cybersecurity/transforming-data-privacy-digital-personal-data-protection-rules-2025); [TCSA roadmap](https://www.tcsa.in/resources/dpdp-rules-2025-implementation-roadmap); [Privy by IDfy](https://www.privybyidfy.com/blog/dpdp-compliance-guide-2026-what-indian-enterprises-must-do-before-may-2027)
- **Exact dates differ by a day:** one source gives 13 May 2027 for the 18-month phase, and another lists the phase dates as 13 Nov 2025, 14 Nov 2026 and 14 May 2027. The Gazette notification is reported as G.S.R. 846(E). — [dcomply DPDP Rules tracker](https://dpdpa.dcomply.in/rules/); [Invield checklist](https://www.invield.com/resources/dpdp-rules-checklist)
- The Rules include **72-hour** breach reporting. — [Cy5 DPDP Rules guide](https://www.cy5.io/blog/dpdp-rules-2025-complete-compliance-guide-cloud-security/)
- **Conflicting outlier:** one guide claims the Rules were notified in January 2025, with 6/12/18/24-month phases. This conflicts with the PIB release and should not be relied on. — [Glocert guide](https://www.glocertinternational.com/resources/guides/dpdp-rules-2025-compliance-timeline/)

### Inferences
- **Timing.** As of 16 Oct 2026, India's core DPDP obligations are about 7 months away. A device and app designed now must ship with these in place:
  - DPDP-compliant notice and consent;
  - security safeguards;
  - a breach-response runbook (72 h);
  - deletion flows;
  - parental consent for users under 18.
- **On-device processing changes the vendor's role.** Under DPDP (prior knowledge, s.3(c)(i)), processing by an individual for personal or domestic purposes is outside the Act. Under GDPR (Recital 18), the household exemption does *not* cover the vendor that provides the processing means. If camera frames are processed only on the device and the company never receives them, the company's data-fiduciary/controller footprint shrinks to account and app data. That is a strong design lever, but it needs legal confirmation.
- **Privacy-by-design for a dressing-area camera** (good practice unless noted):
  1. **On-device inference.** Process frames in RAM only, with no frame storage by default. Persist only derived, non-image data, such as body measurements or style preferences, and only with explicit consent.
  2. **Physical shutter** over the lens, plus a **hardware camera kill switch** that cuts sensor power.
  3. **Hardware-wired camera LED.** Power the LED from the camera sensor's supply rail so firmware cannot turn the camera on without the LED. Never offer a "stealth" or covert mode.
  4. **Camera off by default.** Turn it on per session and switch it off automatically after idle time. Use a narrow field of view aimed at the user. Audio should be off by default.
  5. **No cloud upload by default.** If cloud rendering for virtual try-on is offered:
     - require separate opt-in consent for each feature;
     - use TLS 1.3 in transit and encryption at rest;
     - delete within minutes or hours;
     - **do not use customer images for model training or human labelling** unless there is a separate, explicit, revocable opt-in.
  6. **Account security:**
     - MFA on accounts;
     - no default passwords;
     - least-privilege, logged staff access to any user data, with no routine employee access to images;
     - secure boot and signed OTA updates;
     - a vulnerability-disclosure policy and a published support period.
  7. **Deletion and children:**
     - one-tap "erase everything on this mirror", and account deletion with a defined deadline;
     - per-user profiles;
     - child profiles without try-on, image capture or targeted ads.
  8. **Face recognition is biometric processing.** If the mirror identifies who is standing in front of it, that is biometric identification: GDPR Art. 9 explicit consent and an Illinois BIPA written release (prior knowledge). Default to PIN or profile selection instead. If Face ID-style unlock is offered, keep templates on the device only.
  9. **Marketing claims must match the actual data flows** (e.g., "never leaves your mirror"). Overstated privacy claims are a deceptive-practice risk under FTC Act §5 and India's Consumer Protection Act (prior knowledge).
- **Lessons from enforcement and incidents** (details unverified, see Gaps):
  - Insider access and missing MFA (Ring) → strict staff access control, MFA and audit logging.
  - Development-unit images reaching outside labellers (iRobot) → no images to labellers without explicit consent, including from beta testers.
  - "Local-only" claims contradicted by cloud thumbnails (Eufy) → claims must match the actual data flows.

### Gaps
- No primary text of the DPDP Act or Rules, GDPR, the AI Act or FTC orders could be opened.
- It is unverified whether MeitY has changed the 18-month commencement since mid-2026.
- **Unverified background (prior knowledge; check the official texts):**
  - **India: DPDP Act 2023 (Act 22 of 2023)**
    - [High] **Definitions:** s.2(f) defines a "child" as an individual under 18.
    - [High] **Notice and consent:** s.5 covers notice. s.6 requires consent to be free, specific, informed, unconditional and unambiguous, given by clear affirmative action, and withdrawable as easily as it was given.
    - [High] **Fiduciary duties (s.8):** reasonable security safeguards (s.8(5)), breach intimation to the Board and to affected people (s.8(6)), and erasure when the purpose is served or consent is withdrawn (s.8(7)).
    - [High] **Children (s.9):**
      - (1) verifiable consent of a parent or lawful guardian;
      - (2) no processing likely to harm a child's well-being;
      - (3) **no tracking or behavioural monitoring of children, and no targeted advertising directed at children**;
      - exemptions are possible by rule.
    - [High] **Significant Data Fiduciaries (s.10):** a DPO based in India, an independent data auditor, periodic DPIAs and audits. SDFs are designated by the government based on volume/sensitivity and risk factors.
    - [High] **Penalties (Schedule):**
      - up to **₹250 crore** for failing to take security safeguards;
      - up to **₹200 crore** for failing to report a breach;
      - up to **₹200 crore** for breaching children's obligations;
      - up to **₹150 crore** for breaching SDF obligations;
      - up to **₹50 crore** for other breaches.
  - **India: DPDP Rules 2025** [Med-High]
    - **Draft rules:** the draft Rules were published on 3 Jan 2025. That is likely the source of Glocert's "January 2025" error.
    - **Rule 6 (security):** encryption, obfuscation, masking or tokenisation; access control; logging and monitoring; **retention of logs for 1 year**; backups; contract clauses with processors.
    - **Rule 7 (breach):** notify affected individuals without delay, and the Board without delay with a detailed report within **72 h**.
    - **Rule 10 (parental consent):** verify that the person consenting is an identifiable adult, using reliable identity/age details or a virtual token, e.g., via DigiLocker.
    - **Rule 13 (SDFs):** an annual DPIA and audit, due diligence on algorithmic software, and possible data-localisation restrictions.
    - **Third Schedule:** erasure after 3 years of inactivity for large e-commerce, gaming and social-media platforms.
  - **India: law in force until DPDP s.44 takes effect** [High]
    - IT Act s.43A and the **SPDI Rules 2011**, which classify **biometric information** as sensitive personal data, continue until DPDP s.44(2) omits s.43A at the 18-month commencement [Med].
  - **India: criminal law** [High]
    - **IT Act s.66E** penalises capturing or transmitting images of a person's private area without consent, with up to 3 years' imprisonment or a fine up to ₹2 lakh.
    - **Bharatiya Nyaya Sanhita 2023 s.77** (voyeurism; formerly IPC 354C).
    - A product must never facilitate covert capture.
  - **EU: GDPR** [High]
    - **Definitions:** Art. 4(14) defines biometric data. Recital 51 says photographs count as special-category data only when processed through specific technical means for unique identification.
    - **Special categories:** Art. 9 prohibits processing biometric data for unique identification unless an exception applies, such as explicit consent under Art. 9(2)(a).
    - **Children:** Art. 8 sets the age of digital consent at 13–16 depending on the member state.
    - **Design duties:** Art. 25 requires data protection by design and by default. Art. 35 requires a DPIA for high-risk processing; a camera in private rooms makes a DPIA prudent.
    - **Guidance:** EDPB Guidelines 3/2019 on processing personal data through video devices.
    - **Telemetry consent:** ePrivacy Directive Art. 5(3) requires consent for device telemetry and analytics.
  - **EU: AI Act (Regulation (EU) 2024/1689)** [High unless marked]
    - **Prohibitions** have applied since **2 Feb 2025**. They include:
      - emotion recognition *in workplaces and education* (Art. 5(1)(f)); this does not cover the home;
      - biometric categorisation inferring race, political opinions, religion, sex life or sexual orientation (Art. 5(1)(g));
      - untargeted scraping of facial images (Art. 5(1)(e)).
    - **Transparency:** Art. 50 obligations apply from **2 Aug 2026**, including informing people exposed to emotion-recognition or biometric-categorisation systems.
    - **High-risk:** Annex III(1) lists biometric categorisation and emotion recognition.
    - [Med-High] **Recital 16** says filters that categorise facial or body features on online marketplaces, used so a consumer can **preview a product on themselves**, can be a "purely ancillary feature" outside the definition of biometric categorisation. This is directly relevant to virtual outfit try-on.
    - [Med/Low] **Digital Omnibus:** the Commission's proposal (19 Nov 2025) would delay the high-risk obligations, to about Dec 2027 for Annex III [Med]. **Its adoption status in Oct 2026 is unknown** [Low].
  - **US** [High unless marked]
    - **FTC v. Ring (31 May 2023):**
      - Ring paid **$5.8 million**.
      - The FTC alleged that employees and contractors had broad access to customers' private videos. One employee allegedly viewed thousands of recordings of female users in bedrooms and bathrooms.
      - The FTC also alleged that weak security (no MFA, susceptibility to credential stuffing) let hackers take over cameras.
      - The order requires deleting data, models and algorithms derived from unlawfully reviewed videos, and running a privacy and security program.
      - [Med] The FTC refunded about $5.6M to customers in Apr 2024.
    - **FTC v. Amazon (Alexa), same day:** a $25M COPPA settlement over retention of children's voice recordings.
    - **iRobot (MIT Technology Review, Dec 2022):** Roomba development-unit images, including a woman on a toilet, were sent to outsourced labellers and leaked online.
    - [Med/Low] **Eufy (Anker):** in 2022, cameras marketed as local-only were shown to send thumbnails to the cloud. A regulatory settlement was later reported; check the details.
    - **Illinois BIPA (740 ILCS 14):**
      - requires a written release before collecting face geometry;
      - gives a private right of action for **$1,000 (negligent) or $5,000 (intentional/reckless)** per violation;
      - a 2024 amendment (SB 2979) limits accrual to one violation per person.
    - **Texas CUBI:** enforced by the Attorney General; Meta settled for $1.4B in 2024.
    - **California CCPA/CPRA:** biometric data is "sensitive personal information" with a right to limit its use.
    - **Washington My Health My Data Act:** treats biometric data as consumer health data and gives a private right of action.
    - [Med-High] **COPPA Rule amendments:** finalised in 2025 (effective 23 Jun 2025; compliance by 22 Apr 2026). They add biometric identifiers to "personal information".
  - **Security baselines** [High]:
    - ETSI EN 303 645 (consumer IoT);
    - NISTIR 8259A;
    - [Med] TEC's code of practice for securing consumer IoT (India).

---

## 8. Battery vs mains power for a furniture-sized device

### Takeaway
No battery-specific sources could be retrieved this session. From prior knowledge, a large lithium-ion pack inside an always-on, furniture-sized device in a bedroom or dressing room brings four burdens:
- a thermal-runaway fire risk in an occupied, often sleeping, space;
- additional mandatory certification: IEC 62133-2 / IS 16046 (Part 2) cells under CRS, IEC 62368-1 Annex M and UN 38.3 for transport;
- EPR obligations;
- the EU removability rule from 18 Feb 2027.

In exchange it gives little benefit, because the mirror stays near a socket. **Recommendation: mains-only.** If something must survive power cuts, use at most a small supercapacitor hold-up for graceful shutdown and an RTC coin cell inside a tool-access compartment.

### Cited Findings
- Indian guides list **power banks** among the CRS-regulated (Scheme-II) categories, so lithium energy storage products are under compulsory BIS registration. — [eChai CRS page](https://echai.ventures/d2c/d2c-product-licenses/bis-crs-mark-electronics); [Seyecs CRS guide 2026](https://blogs.seyecs.com/bis-certification-for-electronic-products/)
- No other battery findings could be retrieved: the web-search budget was exhausted.

### Inferences
- **Risk vs benefit.** A battery adds a new class of hazard: chemical energy that can cause fire under abuse or a single fault. It also adds obligations in all three markets, while the product's use case (fixed, wall- or floor-mounted, near a socket) gains little. A UPS-style battery would mainly cover **power cuts**, which are common in parts of India (inference). Software that saves state and recovers cleanly addresses that better than a large battery.
- **If a battery is unavoidable** (e.g., a portable variant) [Good practice]:
  - choose a certified pack with a lower-energy chemistry, such as LiFePO₄ (prior knowledge);
  - add a BMS with redundant protection;
  - mount it in a metal compartment at the bottom, away from the display and the heat of the compute module;
  - test it under IEC 62368-1 Annex M;
  - ship it with UN 38.3 reports;
  - register the cells or pack under CRS in India.

### Gaps
- **Unverified background (prior knowledge):**
  - [High] **Cell and pack standards:**
    - IEC 62133-2:2017 covers the safety of portable sealed secondary lithium cells and batteries. India's adoption, **IS 16046 (Part 2):2018**, is under CRS ("sealed secondary cells/batteries containing alkaline or other non-acid electrolytes").
    - US equivalents are UL 2054, UL 1642 and UL 62133-2.
    - Transport requires UN 38.3 testing.
  - [High] IEC 62368-1 **Annex M** covers equipment containing batteries and their protection circuits.
  - [High] **EU Battery Regulation (EU) 2023/1542:**
    - Art. 11: portable batteries in appliances must be removable and replaceable by the end user from **18 Feb 2027**.
    - [Med] Labelling requirements phase in from Aug 2026.
  - [High] **EPR:** India's Battery Waste Management Rules 2022 impose EPR on producers.
  - [High] **Coin cells:** US Reese's Law (16 CFR 1263, effective 19 Mar 2024) applies to any consumer product containing button or coin cells, which includes an RTC backup cell. IEC 62368-1 cl. 4.8 has similar requirements.
  - **Missing data:** no reliable statistics were gathered on lithium-ion fires in homes or furniture-scale devices.

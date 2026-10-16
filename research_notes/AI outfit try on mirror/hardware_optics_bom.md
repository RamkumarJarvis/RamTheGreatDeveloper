# Hardware, Mirror-Display Optics and Bill of Materials for a Home AI Try-On Smart Mirror

Research date: 16 Oct 2026. Prices are as given by the cited pages (dates shown where the page or search excerpt gave one; "undated" means the listing showed no date when found on 16 Oct 2026). Conversions use an **assumed ₹88 per US$**. This rate is not sourced. For reference, Business Today's Dec 2024 conversion of the LG OLED T price implies about ₹85/US$.

**Method caveat (read first):** WebFetch could not resolve any host in this environment, and the proxy refused direct downloads such as pilkington.com. The shared web-search budget then ran out partway through the research. As a result, every cited finding below comes from search-result excerpts (page titles, snippets and quoted lines), not from full-page reads. Items that could not be searched are listed under Gaps, sometimes with clearly labelled **unverified background estimates** for the report writer to treat as placeholders.

---

## 1. Optics: can a display behind two-way glass "dress" the user's reflection, and how do commercial try-on mirrors solve it?

### Takeaway
Not convincingly. The reflection is a virtual image that sits as far behind the glass as the user stands in front of it, so it is twice as far from the eye as anything drawn on the display. Overlays therefore have a focus mismatch and a fixed two-eye misregistration (about 3 cm on the glass, about 6 cm at body scale). They also need eye tracking to survive head movement. And because a display behind the glass can only add light, it can never darken or hide the real clothes. Commercial try-on mirrors avoid all of this by working as "digital mirrors": a camera films the user and the display shows a corrected, mirror-flipped video with the garment composited into the pixels (MemoMi). Some use a depth camera and AR overlay on the live image, or later an avatar (FXMirror). Overlaying the true optical reflection has stayed at the patent and research stage (Amazon's "blended reality" patent, 3D-Mirrorcle).

### Cited Findings
**Reflection geometry, focus and parallax**
- A display-apparatus patent states that "the focus distance in a case where one's own face is viewed through a mirror would be the distance twice the distance from the face to the mirror. This is because the distance from the mirror reflected to the face is needed in addition to the distance to the mirror." — [USPTO patent 11109015 (search excerpt)](https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/11109015)
- A patent for AR user styling with a semi-transparent mirror describes the ideal case as one where "the focal distance for viewing the reflection image reflected on the semi-transparent mirror unit 130 and the focal distance for viewing the image displayed on the display unit 120 are identical", which implies the default case does not match. — [USPTO patent 10762709, "Device and method for providing augmented reality for user styling" (search excerpt)](https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/10762709)
- MERL's AR survey calls this the "fixed focal length problem". When the real scene and the image plane are at different depths, "the eyes are forced to either continuously shift focus between the different depth levels, or perceive one depth level unsharp". It also notes the problem matters more for see-through displays than for closed-view ones, and that "due to parallax effects virtual objects (e.g., the baby's arm) can appear in front of the mirror". — [MERL TR2006-105, Modern Approaches to Augmented Reality](https://www.merl.com/publications/docs/TR2006-105.pdf)
- 3D-Mirrorcle (2023) states that "directly overlaying a half-mirror on the screen leads to depth mismatch, preventing simultaneously perceiving the screen content and the mirror reflection". Its proposed fix is a lenticular grating that aligns the parallax of separate left- and right-eye views with the viewer's eyes. — [3D-Mirrorcle, arXiv 2310.13617](https://ar5iv.labs.arxiv.org/html/2310.13617)
- The "Augmented Mirrors" paper notes that users rely on motion parallax for depth, and that inaccurate tracking of the mirror-observer relationship makes the mirror view stop matching the virtual view. — [Augmented Mirrors (ResearchGate)](https://www.researchgate.net/publication/344948576_Augmented_Mirrors)

**Additive light only (cannot darken the real clothes)**
- Optical see-through optics "can only add light to the scene, they don't have any way to darken the perceived image, and therefore cannot display an opaque black". This was said of HoloLens-style waveguides, but the same physics applies to a display behind half-silvered glass. — [W3C public-webapps-github archive, Jan 2021](https://lists.w3.org/Archives/Public/public-webapps-github/2021Jan/0735.html)
- With optical see-through displays the user sees "a linear mixture of display and environment light, which creates an impression of transparency unless the displayed color is sufficiently bright". — [Liu et al. 2022, Transparency in AR (Univ. of Cambridge)](https://www.cl.cam.ac.uk/~rkm38/pdfs/liu2022_transparency_in_AR.pdf)
- True occlusion needs an extra light-blocking element. Research examples are Stanford's "Factored Occlusion", which uses a DMD to merge light paths multiplicatively, and FactoredSweeper (ISMAR 2024), which combines attenuation and addition on one spatial light modulator. Both are head-mounted research prototypes, not mirror products. — [Factored Occlusion (computationalimaging.org)](https://www.computationalimaging.org/?p=3737); [FactoredSweeper 2024](https://www.ar.comp.isct.ac.jp/projects/factored-sweeper-2024)

**How commercial try-on mirrors do it**
- MemoMi MemoryMirror (Neiman Marcus, 2015): coverage describes a roughly 70-inch screen with a camera on top filming the shopper, not reflective glass. MemoMi's CEO said the uncorrected image "would look totally distorted", so the company corrects perspective in real time to make the camera appear to sit behind the screen. One report says it also uses three other cameras and patented image-adjustment technology. The frame is brushed stainless steel instead of glass. Shoppers control it from an iPad and it records 8-second videos for side-by-side comparison. — [NPR, 10 Apr 2015](https://www.npr.org/sections/alltechconsidered/2015/04/10/398811812/magic-mirror-at-the-store-should-this-top-go-in-my-drawer); [VentureBeat](https://venturebeat.com/ai/memomis-memorymirror-lets-you-try-on-clothes-without-actually-putting-them-on); [FashionUnited, Jan 2015](https://fashionunited.uk/news/retail/neiman-marcus-debuts-digital-memorymirror/2015011415155); [EDN](https://edn.com/mirror-mirror-on-the-wall-whos-the-most-tech-savvy-of-them-all/)
- FXMirror (FXGear, Korea): coverage says Microsoft Kinect depth cameras are built in. The system estimates the shopper's build from height, weight and facial/body feature points in about 2 seconds. Early versions overlaid 3D garments on the live camera image (AR). A 2018 update switched to an avatar that tracks facial expressions and body movement. A 2019 physics-based simulation compares fits from XS to 3XL. One Singapore installation reportedly cost S$45,000. — [Korea Times, Oct 2018](https://www.koreatimes.co.kr/www/tech/2018/10/133_257518.html); [Newswire (FXGear)](https://www.newswire.com/view/content/fashionable-technology-fxgear-launches-fxmirror-true-fit-the-next-20709876); [Fashnerd, Apr 2019](https://fashnerd.com/2019/04/physics-based-fitting-simulation-to-revolutionise-virtual-fitting-experience/); [Vulcan Post](https://vulcanpost.com/550031/singapore-bridal-virtual-fitting-room-la-belle-couture)
- Amazon "blended reality" mirror patent (reported Jan 2018): a partially reflective, partially transmissive mirror combined with displays, cameras and several projectors that control lighting. It identifies the user's face and eyes to decide what should appear as reflection. Coverage treats it as a patent, not a product. — [GeekWire, 2018](https://www.geekwire.com/2018/amazon-patents-blended-reality-mirror-shows-wearing-virtual-clothes-virtual-locales/); [Engadget, 3 Jan 2018](https://www.engadget.com/2018-01-03-amazon-patent-mirror-virtual-clothes.html); [CNBC, 3 Jan 2018](https://www.cnbc.com/2018/01/03/amazon-patents-a-mirror-that-dresses-you-in-virtual-clothes.html)
- Retail smart mirrors are generally described as a large screen, a camera and virtual try-on software in one fixture: cameras track body position, a display shows the garments, and a compute module runs the image processing. — [GlamAR blog](https://www.glamar.io/blog/magic-mirror-for-retail-how-smart-mirrors-work-in-stores)
- Fraunhofer HHI's virtual mirror "emulates the garment's texture and movement and projects the virtual image onto a screen in front of the shopper". Its shoe mirror could only show a shoe correctly when the foot was flat on the floor. — [The Engineer](https://theengineer.co.uk/content/news/virtual-mirror-shows-new-lines)
- Samsung sold a 55" "mirror display" (ML55E, 2016, FHD) for retail use. It uses a polarized film overlay with "transmittance (90 percent) and advanced reflectance (55 percent)", is rated 400 nits and 24/7 operation, and is now listed as no longer available. Early 2016 coverage gave different numbers (150 nit, 45% transmittance, 75% reflectance), which may describe Samsung Display's mirror OLED panel instead. — [B&H Photo (ML55E)](https://www.bhphotovideo.com/c/product/1266767-REG/samsung_ml55e_55_full_hd.html); [sixteen-nine.net](https://www.sixteen-nine.net/?p=11247); [Multitronic listing (400 nits)](https://www.multitronic.fi/fi/products/1411495/samsung-ml55e-55inch-wide-mirror-display-400nits-speakers-dvi-hdmi-dp-1-2-in-out-rs232-rj45-sssp-gen-3--8gb--wifi-sbb-pc-support); [Knitec (24/7)](https://knitec.com/products/samsung-ml55e-55-direct-lit-led-mirror-display-for-business-with-24-7-operation-and-2-year-warranty); [OLED-info (earlier figures)](https://www.oled-info.com/samsung-display-ship-55-transparent-and-mirror-oleds-q2-2016)

### Inferences
- **Geometry (my derivation from the cited "twice the distance" fact).** With the user's eyes at distance d from the glass, the reflection is at 2d from the eyes and the display graphics are at about d. The focus mismatch is 1/d − 1/(2d) dioptres: **1.0 D at 0.5 m, 0.5 D at 1.0 m, 0.33 D at 1.5 m and 0.25 D at 2.0 m.** So the mismatch is worst exactly where a user leans in to inspect details.
- **Two-eye misregistration (my derivation).** The two eyes' lines of sight to the same point on the reflected body cross the glass plane IPD/2 apart, which is about **31.5 mm for a 63 mm IPD, regardless of distance**. That equals about **63 mm at body scale**, so an overlay can be registered for one eye only and appears doubled or offset to the other. The angular disparity between overlay and reflection is IPD/(2d): **3.6° at 0.5 m, 1.8° at 1 m, 1.2° at 1.5 m and 0.9° at 2 m.** Fixing this needs per-eye images (lenticular or autostereoscopic, as in 3D-Mirrorcle) plus eye tracking, which is research-grade.
- **Additive light.** A virtual garment drawn behind the glass is added to the reflected real garment. A dark virtual top over a white real shirt will look like a ghostly tint over the white shirt. "Dressing the reflection" only works for light or bright overlays such as outlines, highlights, accessories and text, or in a dark room.
- **Design consequence.** For a try-on product, the dependable architecture is a **digital mirror**: camera, segmentation, garment rendering and a mirror-flipped video on the display. The two-way glass is then only a styling element for "mirror mode" when the try-on is not running. During try-on the display must overpower the glass reflection, otherwise the user sees a double image (real reflection at 2d plus video at d). Section 2 quantifies this.
- **The camera viewpoint problem moves to software.** A top-mounted camera sees the user from above, so the video must be perspective-corrected (the MemoMi approach) or the camera must sit near eye level behind or through the glass (Section 7).
- **The polariser trick is worth noting.** LCD output is already polarised, so a reflective-polariser mirror film (as the Samsung ML55E "polarized film overlay" appears to use) can pass about 90% of the LCD's light while still reflecting about 55% of ambient light. That is a much better display-to-reflection trade-off than a neutral 70/30 two-way mirror. This is my interpretation of the 90%/55% figures, and the sources do not explain the mechanism.

### Gaps
- Could not read the full 3D-Mirrorcle, MERL or Augmented Mirrors papers (fetch blocked), so none of their quantitative results are included.
- No current (2024-2026) sources on MemoMi, FXMirror or other commercial try-on mirrors' hardware specs. The coverage found is 2015-2019.
- No primary source found that explicitly says "consumer smart mirrors use a camera feed because overlays cannot align with the reflection". The conclusion above is inferred from the optics sources and product descriptions.

---

## 2. Display brightness needed behind two-way glass for the screen image to dominate the reflection

### Takeaway
It depends mainly on the glass's reflection/transmission split and the room lighting. For a 500-lux room and medium-reflectance clothing, my calculation from the cited inputs (Inferences below) gives these panel luminances for a 5:1 display-to-reflection ratio: about **1,060 nits** behind standard MirroView (about 21% T / 70% R), about **430 nits** behind MirroView 50/50 (37% T / 50% R), about **740 nits** behind 70/30 acrylic, about **210 nits** behind a 40/60 "dielectric" glass, and about **195 nits** with a polariser-type mirror (90% T for LCD light). A typical 300-400-nit consumer TV behind standard MirroView cannot hide even the reflection of a white shirt. Hence the choice for try-on is a high-transmission glass (50/50, 40/60 or a polariser film) plus a 500-700+ nit signage panel, or no mirror glass over the try-on area.

### Cited Findings
- **Pilkington installation guidance:** the coating should face the viewer, and the display should be turned up to compensate for the transmission loss. — [Pilkington ATS-191 MirroView Design/Fab/Install bulletin (2015)](https://www.pilkington.com/~/media/Pilkington/Site%20Content/USA/Architects/ATS%20191%20MirroView%20Design%20Fab%20Install%202015%2004%2017%20NSG%20format.pdf)
- **Community guidance (MagicMirror forum):** choose transmission by room. Dark rooms: about 4-10%. Normally lit rooms without direct sun: 12-20% ("sweet spot is 12% when balancing readability and backlight bleed through"). Public or daylit spaces: 30-50%. A normal mirror reflects about 85-98%; "Most two way mirrors has around 60%, often lower." — [MagicMirror forum thread](https://forum.magicmirror.builders/post/48954)
- A builder reports that backlight bleed (the dark-grey glow of an LCD showing "black") is invisible as long as the room in front of the mirror is brighter than the monitor behind it, and shows up only with the room lights off. — [MagicMirror forum](https://forum.magicmirror.builders/post/45961)
- A smart-home calculator suggests adding about 50% to the brightness target to offset a 30-50% loss through mirror film, and gives 300-700 nits as a typical smart-mirror range. Its methodology is unverified, and its 30-50% loss conflicts with the 63-80% loss implied by MirroView's 20-37% transmission. — [DIY Smart Home Hub lux-to-nits calculator](https://www.diysmarthomehub.com/lux-to-nits-converter/)
- **Luminance of a diffuse surface:** L = ρE/π (cd/m²), with E in lux and ρ the reflectance. Worked example: 500 lux on a 0.4-reflectance surface gives 200 apostilbs, about 64 cd/m². — [Wikipedia: Luminance](https://en.wikipedia.org/wiki/Luminance); [Cornell DEA3500 lighting notes](https://ergo.human.cornell.edu/studentdownloads/DEA3500notes/Lighting/lightingnotes1.html)
- Samsung ML55E mirror display (polariser film): 90% transmittance, 55% reflectance, 400 nits panel (see Section 1 sources).

### Inferences
Worked numbers (my calculation): room or front lighting of E = 500 lux on the user. Clothing luminance L = ρE/π is about 8 cd/m² for black cloth (ρ = 0.05), 32 for dark (0.2), 64 for mid (0.4) and 127 for white (0.8). The reflected luminance is R × L, and the display seen through the glass is T × panel nits.

| Glass (R / T from Section 4 sources) | Reflection of mid-tone clothing | Panel nits for 3:1 | 5:1 | 10:1 | 400-nit TV vs white-shirt reflection |
|---|---|---|---|---|---|
| MirroView standard (~70% / ~21%) | 45 cd/m² | ~640 | ~1,060 | ~2,120 | 84 vs 89 cd/m² (display loses) |
| MirroView 50/50 (~50% / ~37%) | 32 cd/m² | ~260 | ~430 | ~860 | 148 vs 64 (2.3:1) |
| Acrylic two-way (~70% / ~30%) | 45 cd/m² | ~450 | ~740 | ~1,490 | 120 vs 89 (1.35:1) |
| "Dielectric" bright-room glass (~40% / ~60%) | 25 cd/m² | ~130 | ~210 | ~420 | 240 vs 51 (4.7:1) |
| Polariser mirror, ML55E-type (~55% / ~90% of LCD light) | 35 cd/m² | ~120 | ~195 | ~390 | 360 vs 70 (5.1:1) |

- These are luminances of the rendered garment pixels. Mid-tone garments are rendered well below panel white, so the panel's peak brightness needs headroom of roughly 2× on top of these figures.
- **Design conflict:** the high-CRI front lighting needed for judging colour (Section 9) also brightens the user's reflection, which the display then has to beat. The options are to dim the mirror's own lighting during try-on, to use high-transmission glass, or to leave the try-on window as plain anti-reflective glass.
- The trade-off is reversed in "mirror mode": high-transmission glass makes a weaker mirror and shows more backlight bleed in dim rooms (forum guidance above). A 50/50 or polariser solution is a middle ground. An OLED or local-dimming panel would reduce bleed, but its brightness through glass is lower.

### Gaps
- No manufacturer specification of nits required for MirroView or MirroView 50/50 was found. Pilkington's bulletin only says to "turn up" the display.
- No measured data was found on the reflectance of real clothing under typical Indian home lighting. The 500-lux and ρ values are assumptions.

---

## 3. The "half-height" rule and what it implies for portrait screen size

### Takeaway
A flat mirror only needs to be half the viewer's height to show the whole body, whatever the viewing distance. A 180 cm person needs a 90 cm reflective span from about 84 cm to 174 cm above the floor. For a digital mirror rendered at true mirror scale, the person's image on the screen plane is likewise half-size. So the active portrait display height should be at least H/2: a **43" portrait panel (95.2 cm tall) is the bare minimum for a 190 cm user, 50" (110.7 cm) is comfortable, and 55" (121.8 cm) leaves room for UI.**

### Cited Findings
- The law of reflection puts the mirror's bottom edge halfway between the feet and the eyes, and its top edge halfway between the eyes and the top of the head. The mirror therefore needs to be half the person's height, "with two pairs of congruent triangles, the height of the vertical reflector should be half his height", and "the distance from the mirror doesn't matter". A 180 cm person needs at least 90 cm of mirror. — [University of Illinois Physics Van Q&A "Mirror, Mirror, On the Wall"](https://van.physics.illinois.edu/ask/listing/1936); [Physics Forums](https://www.physicsforums.com/threads/minimum-height-of-a-vertical-reflector.914612/post-5762109); [Vedantu worked problem (180 cm man)](https://vedantu.com/jee-main/a-man-is-180cm-tall-and-his-eyes-are-10cm-below-physics-question-answer)

### Inferences
- **Required mirror span (my calculation; eye height assumed 10-12 cm below the top of the head):** 160 cm person: 0.74-1.54 m; 170 cm: 0.79-1.64 m; 180 cm: 0.84-1.74 m; 190 cm: 0.89-1.84 m. Covering everyone from 160 to 190 cm with a fixed real mirror needs the band **0.74-1.84 m (1.10 m tall)**.
- **16:9 panel sizes in portrait (my calculation):** 43" = 95.2 × 53.5 cm; 50" = 110.7 × 62.3 cm; 55" = 121.8 × 68.5 cm; 65" = 143.9 × 80.9 cm.
  - A 55" portrait panel with its bottom edge about 0.65 m above the floor covers 0.65-1.87 m, which spans the whole 160-190 cm user range in optical (mirror) mode.
  - A 50" panel just covers 0.74-1.85 m.
  - A 43" panel cannot cover all heights at once, but in a digital mirror the image can be shifted in software.
- A digital mirror is free to scale the image, but a "life-size" mirror feel needs about H/2 of on-screen height, so screen height still matters. A full-length dressing-mirror frame (about 150-180 cm of glass) can be larger than the display. The display only needs to sit behind the try-on zone.
- The camera viewpoint must be re-projected toward the user's eye position for the digital image to have mirror-like perspective, as MemoMi does (Section 1).

### Gaps
- No source was found on preferred display size or scale in commercial try-on mirrors, beyond MemoMi's roughly 70-inch screen.

---

## 4. Smart-mirror glass options: Pilkington MirroView, MirroView 50/50, other dielectric "mirror TV" glass, acrylic, film; R/T, thickness, safety, prices

### Takeaway
Pilkington MirroView is the reference "mirror TV" glass: about 20-22% transmission and 66-74% reflection, in 3/3.2 mm and 6 mm. MirroView 50/50 (about 37% T / about 50% R, 6 mm only per a 2015 bulletin) is meant for bright rooms and suits try-on far better. Acrylic two-way mirror (about 70/30) is light and shatter-resistant but flexes and distorts at full-length sizes. Higher-transmission "dielectric" glass (about 40% R / 60% T) exists for very bright rooms. Indian market pricing for proper display-grade two-way glass was not found. IndiaMART "one-way/reflective" glass ranges from ₹75 to ₹2,900 per sq ft, which is about ₹1,100-42,000 for a 1.8 × 0.75 m mirror, but those are not necessarily display-optimised coatings.

### Cited Findings
- **MirroView (standard):** a trade article gives about 22% light transmission and about 66% coated-side reflection. A Pilkington technical bulletin gives about 20% visible transmission and 74% reflectivity, with 68% from the glass side. Pilkington's product page lists available thicknesses of 3.2 mm and 6 mm. — [Glass Online, "Interactive mirrors with Pilkington MirroView"](https://www.glassonline.com/interactive-mirrors-with-pilkington-mirroview/); [Pilkington ATS-191 (2013)](https://www.pilkington.com/-/media/pilkington/site-content/usa/window-manufacturers/technical-bulletins/ats191mirroviewdesignfabinstall20130107.pdf); [Pilkington MirroView product page](https://www.pilkington.com/en/global/products/product-categories/special-applications/pilkington-mirroview)
- **MirroView 50/50:** about 37% light transmission and about 50% coated-side reflection, "designed for applications in high brightness environments". Per the 2015 bulletin it was then available only in 6 mm (standard: 3 mm and 6 mm). — [Glass Online](https://www.glassonline.com/interactive-mirrors-with-pilkington-mirroview/); [Pilkington ATS-191 (2015)](https://www.pilkington.com/~/media/Pilkington/Site%20Content/USA/Architects/ATS%20191%20MirroView%20Design%20Fab%20Install%202015%2004%2017%20NSG%20format.pdf)
- NSG Group (Pilkington) and Visualplanet showed an integrated smart mirror at ISE 2017: MirroView plus touchfoil working through glass up to 10 mm with 6 ms response. — [Pilkington news, ISE 2017](https://my.pilkington.com/en/news-insights/latest/nsg-group-and-visualplanet-to-exhibit-integrated-smart-mirror-at-ise-2017)
- **Other vendor glass (TwoWayMirrors.com, per 2016 forum posts):** smart-mirror glass "at 30% transparency". A "Vanity Glass" at about 70% reflection / 25% transmission. A "Dielectric" glass at about 40% reflection / 60% transmission, "designed for very bright rooms". — [MagicMirror forum post 132](https://forum.magicmirror.builders/post/132); [MagicMirror forum thread](https://forum.magicmirror.builders/post/48954)
- **Acrylic two-way mirror:** TwoWayMirrors gives about 70% reflective / 30% transparent. Mirrorworld gives roughly 80-95% reflection, and MaterialDistrict gives 85-90% for "see-thru" acrylic, so figures vary by vendor. Acrylic is lighter and more impact-resistant but "less rigid, which can distort in large sheets". A glass vendor says glass is "the more effective choice for most projects". — [TwoWayMirrors acrylic PDF](https://www.twowaymirrors.com/wp-content/uploads/2019/02/acrylic-two-way-mirror.pdf); [Mirrorworld acrylic two-way PDF](https://mirrorworld.co.uk/PDF/Acrylic%20Two%20Way%20Mirror.pdf); [MaterialDistrict](https://materialdistrict.com/material/see-thru-acrylic-mirror/); [TwoWayMirrors catalog 2023](https://www.twowaymirrors.com/catalog/two-way-mirrors-catalog-2023.pdf)
- **Camera behind glass:** TwoWayMirrors says "transparency translates into picture quality". Its glass two-way mirror at 11% transparency "blocks almost all of the light". It recommends a shroud on the camera side. — [TwoWayMirrors: hide camera behind mirror](https://www.twowaymirrors.com/hide-camera-behind-mirror/)
- **India listings (IndiaMART seller listings, undated):**
  - One-way blue mirror, 5 mm: ₹75/sq ft (Bengaluru).
  - One-way black window mirror, 4 mm: ₹2,900/sq ft (Moradabad).
  - Reflective glass, 5 mm: ₹78/sq ft (Ghaziabad).
  - A "smart TV mirror" at ₹1,75,000.
  - [IndiaMART reflective glass](https://m.indiamart.com/impcat/reflective-glass.html); [IndiaMART window mirror](https://m.indiamart.com/impcat/window-mirror.html); [IndiaMART mirror glass](https://m.indiamart.com/impcat/mirror-glass.html); [IndiaMART mirror TV](https://m.indiamart.com/impcat/mirror-tv.html)
- **Indian market context:** "good LED mirror" (backlight only) ₹4,000-12,000; smart mirror with touch display ₹30,000-80,000. — [StudioMatrx smart bathroom mirror India guide](https://www.studiomatrx.org/guides/smart-bathroom-mirror-india)
- **Global, ready-made kits:** TwoWayMirrors sells smart-mirror PCAP foil and complete systems with "a complete parts list and step-by-step guide, as well as pricing for complete systems" (see Section 6 for the foil price). — [TwoWayMirrors PCAP foil](https://www.twowaymirrors.com/pcap-foil/)

### Inferences
- **Recommended for try-on: MirroView 50/50 (6 mm) or a 40/60 dielectric glass.** Standard MirroView (about 21% T) is designed for info overlays in mirror mode and would need a display of over 1,000 nits to dominate the reflection (Section 2).
- **Glass size and weight (my calculation; soda-lime glass density of about 2,500 kg/m³ is a standard value, not sourced here):**
  - 6 mm glass weighs about 15 kg/m².
  - A full-length 1.8 × 0.75 m mirror (1.35 m², about 14.5 sq ft) weighs about 20 kg.
  - A 55"-sized panel (0.83 m², about 9 sq ft) weighs about 12.5 kg.
  - Add a 55" TV and the frame, and the assembly is roughly 35-50 kg, so wall anchoring is mandatory.
- **Indian price spread (my calculation):** at the IndiaMART per-sq-ft rates, the full-length mirror would cost about ₹1,100-42,000. The ₹75-78 listings are almost certainly ordinary reflective/solar-control glass, not display-grade two-way glass, and their R/T is unknown. Request R/T datasheets and a sample, or import MirroView, Guardian or AGC-type product.
- **Acrylic** is acceptable for a small prototype window over the display. For a full-length dressing mirror, flex-induced distortion of the reflection defeats the purpose unless it is bonded to a rigid backer.

### Gaps
- **Prices:** no price found for Pilkington MirroView or MirroView 50/50, in India or globally (pilkington.com and twowaymirrors.com could not be fetched, and the search budget ran out).
- **Toughening and lamination:** not confirmed for MirroView or 50/50. Unverified background: MirroView uses a pyrolytic hard coating and is widely sold as toughenable and laminatable. Verify with NSG/Pilkington India.
- **Other makers:** no data on other makers' "mirror TV" glass (e.g. Guardian, AGC, Saint-Gobain, Chinese dielectric "smart mirror glass" on Alibaba), including R/T, thickness, MOQ or price.
- **Two-way mirror film on clear glass:** no sourced R/T or price data. Unverified background: most "one-way" window films are metallised, perform poorly at night or when the room is darker than behind the glass, and add a slight blue/grey cast.
- **Indian safety rules:** none found for full-length glass mirrors in homes. Background inference: use toughened or laminated glass, or a safety-backing film.

---

## 5. Displays: consumer 4K TVs vs commercial signage vs transparent OLED/LCD; Indian prices

### Takeaway
For a prototype, a 43-55" consumer 4K TV is by far the cheapest option in India: about ₹16,500-24,000 for 43" and about ₹26,700-34,000 for 55" (Jun-Jul 2026 listings). These TVs are not rated for portrait or 24/7 use, and are typically around 300-400 nits (unverified). A commercial 500-nit, 24/7, portrait-rated 55" signage panel such as the Samsung QM55C costs about US$1,260 in the US but ₹2.41 lakh through an Indian importer. Transparent OLED (LG 55EW5 series, about 38-43% transparency, 150-600 nits, US$16k-37k; LG Signature OLED T 77", US$59,999) does not solve the mirror problem. It shows whatever is behind it, still only adds light, and costs 50-200× a TV.

### Cited Findings
**Indian consumer TV prices (aggregator snapshots)**
- **43" 4K:**
  - Kenstar 43UHDTDKEETB, ₹16,499 on Flipkart (list updated 20 Jul 2026). — [Smartprix Kenstar list](https://www.smartprix.com/tvs/kenstar-brand)
  - realme TechLife 43" QLED 4K (2026 edition), ₹21,999 on Flipkart (low ₹21,499). — [PriceBefore](https://www.pricebefore.com/realme-techlife-108-cm-43-inch-p1018574.html)
  - Hisense 43A6K, ₹23,990 on Flipkart (updated 4 Jun 2026). — [MySmartPrice](https://www.mysmartprice.com/electronics/hisense-43a6k-43-inch-uhd-smart-led-tv-msf612241)
- **55" 4K:**
  - Blaupunkt CyberSound G2 55", ₹26,699; Acer V Series AR55GR2851VQD 55" QLED, ₹30,399; TCL 55C645, ₹35,899; Vu Vibe, ₹35,990 (MySmartPrice price list, Jun 2026). — [MySmartPrice 50-59" TV price list](https://www.mysmartprice.com/electronics/pricelist/50-inch-led-tv-price-list-in-india.html)
  - Hisense E6N 55" 4K Google TV on Amazon, ₹28,499 (tracker's all-time low; high ₹38,999; undated). — [PriceHistory](https://pricehistoryapp.com/product/hisense-139-cm-55-inches-e6n-series-4k-ultra-hd-smart-led-google-tv-black)
  - Vu GloQLED 55" 4K, ₹33,999 (roundup dated 10 Jul 2026). — [MagicDrop](https://magicdrop.in/drops/55-inch-qled-tv)
  - NU LED55QUGNX 55" 4K QLED, ₹33,999 (Smartprix, updated 27 May 2026). — [Smartprix NU](https://www.smartprix.com/tvs/nu-brand/price-30000_to_40000)

**Commercial signage**
- Samsung QM55C: 55" 4K, 500 nits typical, "24/7 operation support … continuous commercial use in both landscape and portrait orientations". — [CrownTV blog](https://crowntv-us.com/blog/samsung-qm55c/)
  - US: US$1,260 sale (regular US$1,660) at CompSource, Avendor and Full Compass; US$1,660 at AVI-SPL. — [CompSource](https://www.compsource.com/buy/QM55C/389); [Full Compass](https://www.fullcompass.com/prod/625803-samsung-qm55c-55-commercial-4k-uhd-display); [Avendor](https://www.avendor.com/products/55-inch-commercial-4k-uhd-display-500-nit); [AVI-SPL](https://shop.avispl.com/products/samsung-qm55c-55-full-hd-smart-commercial-signage-display)
  - India: ₹2,41,105 "includes GST and import duties" (Tanotis, undated). — [Tanotis QM55C](https://www.tanotis.com/collections/commercial-monitors-displays/products/samsung-qm55c-55-uhd-4k-commercial-monitor)
- **Portrait mounting:** portrait VESA mounts are marketed for signage, e.g. a StarTech portrait mount for 40-55" screens, and mount warranties exclude "improper installation or application". No consumer-TV maker statement on portrait use was found. — [CDW StarTech portrait mount](https://cdw.com/product/startech.com-portrait-tv-mount-40-55-vesa-tilting-vertical-tv-wall-mount/6618196); [Infinite Cables portrait mount](https://us.infinitecables.com/products/fixed-portrait-tv-wall-mount-bracket-for-flat-lcd-led-fits-sizes-45-70-inches-maximum-vesa-600x400)

**Transparent OLED**
- **LG 55EW5G:** 400 nits typical at 25% APL (without glass); 38% transparency (2018 measurement); listed at US$36,851. LG states transparent LCD manages about 10% transparency, versus higher for its OLED. — [commercialdisplay.sg LG 55EW5G](https://commercialdisplay.sg/digital-signage/lg-55ew5g/)
- **LG 55EW5PG-S:** discontinued, US$16,250 sale (was US$21,666). — [Creation Networks](https://creationnetworks.net/products/lg-ew5pg-s-55-class-full-hd-transparent-oled-signage-display)
- **LG 55EW5TF-A (touch):** 400 nits, 33% transparency. — [Adorama](https://www.adorama.com/loc55ew5tfa.html)
- **LG 55EW5P-M:** 200/600 nits (100%/25% APL), 43% transparency, about US$17,333 (list US$21,667). — [Kickstart Computers](https://kickstartcomputers.com.au/shop/displays/digital-signage-interactive-displays/lg-55ew5p-m-55-transparent-oled-signage/); [Full Compass](https://www.fullcompass.com/prod/638659-lg-electronics-55ew5p-m-55-transparent-oled-commercial-display)
- **LG 55EW5Q-C:** 200/600 nits, 43% transparency, MSRP US$20,000. — [Almo Pro AV](https://www.almoproav.com/productdetails/LGPRO/55EW5Q-C)
- **Resolution:** the 55" LG transparent OLED is 1920×1080. — [SHI listing](https://www.publicsector.shidirect.com/product/50396511/55IN-TRANSPARENT-OLED-1920X1080-HDMI-DP-RS-232C-RJ45-WEBOS7.5)
- **Planar LookThru LO552 (55"):** 38% transmissivity; MSRP US$14,333; CDW US$11,752.54. — [CDW-G](https://cdwg.com/product/plasmon-planar-lookthru-lo552-55-transparent-oled-display/7600286); [Creation Networks](https://creationnetworks.net/products/planar-lo552-55-lookthru-transparent-oled-display)
- **Chinese 55" transparent OLED:** about 40% transmittance, US$5,070-5,719. — [Viperatech](https://www.viperatech.com/product/transparent-oled-display-55-inch-self-luminous-splicing-transparent-screen-hd-commercial-exhibition-touch/)
- **LG Signature OLED T:** 77" 4K, switchable between transparent and opaque, US SRP US$59,999 at select retailers. No Indian launch confirmed; Business Today converts the price to about ₹51.1 lakh. — [CE Pro](https://www.cepro.com/audio-video/lg-77-inch-signature-oled-transparent-display-costs-60k); [OLED-info](https://oled-info.com/lg-starts-offering-its-transparent-signature-oled-t-tv-60000-price-tag); [Business Today, 26 Dec 2024](https://www.businesstoday.in/amp/technology/news/story/lg-unveils-worlds-first-transparent-tv-signature-oled-t-that-costs-as-much-as-a-delhi-house-458568-2024-12-26)

**Power**
- An EU energy fiche for a 43" 4K TV (Toshiba 43UL2063DB) lists 54 W on-mode, 78 kWh/yr at 4 h/day, and 0.5 W standby. — [BT energy fiche PDF](https://m.businessdirect.bt.com/images/EnergyComplianceInfo/FY5V/EnergyFicheURL/631257_fiche-27924.pdf)
- A Dutch source says 55" 4K HDR sets use at least 70-90 W. — [Webwoordenboek](https://webwoordenboek.nl/kenniscentrum/hoeveel-watt-is-een-4k-tv)

### Inferences
- **Prototype choice:** a 55" 4K consumer TV (₹27k-34k) behind MirroView 50/50 or dielectric glass. It is bright enough only with dimmed room or front lighting during try-on (Section 2). Mounting it in portrait is at your own risk: no warranty or thermal guidance was found.
- **Product choice:** a 500-700-nit, portrait-rated, 24/7 or 16/7 panel or open-cell module (QM55C class), or an ODM open-cell panel with a custom backlight. The Indian importer price (₹2.41 lakh, about 2.2× the US$1,260 US street price at ₹88/$) shows that one-off imported signage is very expensive in India. Volume buys should go direct through OEM/ODM channels.
- **Why transparent OLED/LCD does not fit this use:**
  1. A transparent panel shows the wall behind it, not the user. To act as a mirror, a mirror would have to go behind it, and the user's reflection would then pass through the panel twice (about 0.43² ≈ 18% of the light).
  2. Graphics are still on one plane (the same focus and parallax problem) and still additive.
  3. It is FHD only at 55".
  4. It costs US$5k-60k.
  - Transparent LCD is worse still: about 10% transparency and it needs a bright backlight box.

### Gaps
- No 50" Indian TV prices were captured.
- No measured brightness (nits) was found for the budget Indian TVs listed. Unverified background: typical non-HDR-flagship LCD TVs are around 250-400 nits SDR.
- No Indian distributor or B2B price was found for Samsung QM/QB-series or LG UH-series signage, and no 16/7-duty model data was found (e.g. Samsung QB series).
- Open-frame or open-cell panel prices were not researched (search budget exhausted).
- No transparent LCD price data was found.
- No consumer-TV warranty language on portrait mounting was found.

---

## 6. Touch through glass: IR frames vs projected-capacitive (PCAP) foil; touchless alternatives

### Takeaway
IR frames are cheap (about US$50-160 per 55" frame on Alibaba at MOQ 10; about US$160-300 retail) and work regardless of glass thickness, but they add a raised bezel on top of the glass. PCAP foil is invisible behind the glass but limited by thickness. Visualplanet quotes 10 mm (multi-user), 15 mm (kiosk) or 20 mm (single-user). It is expensive at retail (about US$1,977 for a 55" smart-mirror foil). For a try-on mirror where users stand 1-2 m away, touchless control (gestures from the existing camera, plus voice) is the more natural primary input. Touch is optional.

### Cited Findings
- **Visualplanet touchfoil maximum glass thickness:**
  - Single-User touchfoil: consistent touch "in thicknesses up to 20mm". — [Installation International (ISE Daily)](https://www.installation-international.com/ise-daily/single-user-touchfoil-rugged-environments)
  - Multi-user touchfoil: "6 ms touch performance through glass of up to 10 mm" (NSG/Visualplanet, ISE 2017). — [Pilkington news](https://my.pilkington.com/en/news-insights/latest/nsg-group-and-visualplanet-to-exhibit-integrated-smart-mirror-at-ise-2017)
  - 2015 kiosk touchfoil: "designed to work with glass up to 15 mm thick". — [Digital Signage Today](https://www.digitalsignagetoday.com/news/visualplanet-releases-customizable-touchfoil-for-multitouch-kiosks/)
- **PCAP foil prices:**
  - TwoWayMirrors 55" PCAP foil, US$1,976.87 (undated). — [TwoWayMirrors PCAP foil](https://www.twowaymirrors.com/pcap-foil/)
  - Pro Display sells single- and dual-touch foils in sizes including 55", quote only. — [Pro Display PCAP touch foil](https://prodisplay.com/touch-screens/interactive-overlays/pcap-touch-foil/); [Pro Display PDF](https://prodisplay.com/wp-content/uploads/2022/04/Interactive-PCAP-Touch-Foils.pdf)
  - An auto-generated aggregator claims "from $102 for 55" units", which is unreliable. — [Accio](https://www.accio.com/business/optical-touch-foils)
- **IR touch frame prices (55"):**
  - Alibaba: a Hangzhou Ingscreen 10/20-point frame at US$51-164 (MOQ 10); an overlay kit at US$41-514.7; a Guangzhou Hua Chu 32-55" kit at US$27-81. — [Alibaba IR touch screen frame overlay](https://electronics.alibaba.com/product/ir-touch-screen-frame-overlay)
  - Newegg: Senisway 55" 20-point frame at US$298 (US$297.99). — [Newegg](https://www.newegg.com/p/3C6-05G2-01AA3)
  - Newegg Australia: 55" 10-point frame at AUD 638, glass not included. — [Newegg AU](https://www.newegg.com/global/au-en/p/2NY-004T-00031)
  - Desertcart Singapore: deyowo 55" at S$459. — [Desertcart SG](https://www.desertcart.sg/products/223338655-55-inch-ir-touch-frame.md)
  - eBay: a 55" IR frame at US$160. — [eBay store](https://www.ebay.com/str/professionaltouchscreenstore)

### Inferences
- **IR frame trade-offs.** It senses touch in a light-curtain just above the glass, so glass thickness does not matter. But the frame's raised lip conflicts with a flush, frameless mirror look, and anything near the surface (sleeves, hair, hanging garments) can trigger it. These failure modes are generic knowledge of IR frames, not sourced here.
- **PCAP trade-offs.** PCAP behind 6 mm MirroView 50/50 is within all of Visualplanet's limits. Through-glass sensing may also depend on the coating being non-conductive (dielectric). That is unverified; check with the foil vendor.
- **User-flow argument (inference).** Try-on happens at 1.5-2 m, where the camera already tracks the body. So hand-gesture selection (e.g. hover or pinch detected by pose and hand-landmark models) plus voice ("show me the blue kurta") avoids walking up to touch. A cheap IR frame can be kept for close-range menus in the prototype.

### Gaps
- No India-sourced IR frame or PCAP foil prices were found (search budget exhausted).
- No accuracy or latency specs were found for IR frames.
- No official Visualplanet datasheet was found; the thickness figures come from press coverage.
- No data was found on PCAP performance through metallic vs dielectric mirror coatings.
- Touchless options (MediaPipe-style hand tracking, voice stacks) were not researched for this section.

---

## 7. Cameras: options, field of view, depth range, price; placement and the FOV needed for a full body at 1.5-2 m

### Takeaway
To frame a full body (a 2.0 m tall zone) at 1.5 m, a camera at mid-height needs about **67° of vertical FOV**, falling to about 53° at 2.0 m. A camera on the top bezel needs about 55° (tilted about 24° down) but sees the user from above, so the image needs perspective correction. Mount the camera **rotated 90°** so its wide axis is vertical.
- **Raspberry Pi Camera Module 3 Wide** (102° × 67°, about US$32-35) covers the zone easily and is the cheapest option.
- **Logitech C920** (78° diagonal, about 70° × 43°; US$68-70; India C920s ₹7-8k) only just fits at 1.5 m.
- **Depth cameras** help body measurement and segmentation:
  - Orbbec Gemini 335: US$264, 90° × 65°, optimal 0.26-3 m.
  - RealSense D435i/D455: 87° × 58°; £434 / £543 ex-VAT in the UK. RealSense was spun out of Intel on 11 Jul 2025.
  - Orbbec Femto Bolt: ToF, 120° WFOV, 0.25-5.46 m; ₹69,920 in India.
  - Luxonis OAK-D Lite: US$269 (VAT incl.), on-board 4 TOPS.
  - Luxonis OAK-D Pro: US$536.25, 80° × 55°.

### Cited Findings
- **Raspberry Pi Camera Module 3 Wide:**
  - Diagonal 120°, horizontal 102°, vertical 67°. — [Core Electronics product page](https://core-electronics.com.au/raspberry-pi-camera-v3-wide-angle.html.md); [Circuit.Rocks](https://circuit.rocks/products/raspberry-pi-camera-module-3-12mp-120-degree-wide-angle-lens)
  - Prices: AU$62.00 incl. GST at Core Electronics; 499 SEK incl. VAT at Electrokit; DKK 349 at RaspberryPi.dk. A Polish tracker shows about US$32-35 across late 2024-2025. — [Electrokit](https://www.electrokit.com/en/raspberry-pi-kameramodul-3-12mp-120); [RaspberryPi.dk](https://raspberrypi.dk/?p=173811); [Elecena price history](https://elecena.pl/product/27036821/rss)
- **Logitech:**
  - The C920 has a fixed 78° FOV; the Brio 4K is adjustable to 65°, 78° or 90°. — [Synced.sg Brio vs C920](https://synced.sg/blogs/news/logitech-brio-vs-c920); [Ceedo](https://www.ceedo.com/logitech-c920-vs-brio/)
  - US prices: C920 about US$68-70, Brio about US$168-200. — [TheTechShowdown](https://thetechshowdown.com/compare/logitech-brio-4k/logitech-c920-hd-pro)
  - India: C920s ₹6,999-7,999. — [GetPC.co.in](https://getpc.co.in/parts/webcam/logitech-c920s)
- **RealSense:**
  - Corporate: RealSense, Inc. "completed its spinout from Intel" on 11 Jul 2025, with a US$50M Series A that included Intel Capital and MediaTek Innovation Fund. Wikipedia, citing Calcalist (Sep 2026), reports that Cognex is buying RealSense for US$600M. That is single-source and unverified. — [Intel RealSense overview](https://www.intel.com/content/www/us/en/architecture-and-technology/realsense-overview.html); [Wikipedia: RealSense](https://en.wikipedia.org/wiki/RealSense); [eWeek on the spinoff's robotics focus](https://www.eweek.com/fr/news/news-intel-spinoff-realsense-ai-humanoid-robots/)
  - Specs:
    - D455: depth FOV 87° × 58° (±3°), 0.6-6 m. — [Robotics Center D455](https://www.roboticscenter.ai/ar/store/product/intel-realsense-d455)
    - D455: 0.4 m minimum, 20 m maximum range. — [RS Philippines D455](https://ph.rs-online.com/web/p/depth-cameras/2026353)
    - D435: 0.105 m minimum, 10 m maximum. — [RS UK D435](https://uk.rs-online.com/web/p/depth-cameras/1720981)
    - D435if: 0.3-3 m. — [RS Philippines D435if](https://ph.rs-online.com/web/p/depth-cameras/0155773)
  - Prices:
    - RS UK: D435i £434.00 and D455 £543.30, both ex-VAT and "temporarily out of stock". — [RS UK RealSense](https://uk.rs-online.com/web/b/realsense/)
    - RS Netherlands: D455 €622.30 ex-VAT. — [RS NL](https://benl.rs-online.com/web/b/realsense)
    - Switch Science (Japan): D455 ¥106,293, D435i ¥95,282, tax included. — [Switch Science RealSense](https://www.switch-science.com/collections/all/cat-%E3%83%96%E3%83%A9%E3%83%B3%E3%83%89%E5%B0%8F%E5%88%86%E9%A1%9E_realsense)
    - An Alibaba aggregator gives about US$300-350 (D435i) and US$380-450 (D455). That source is low-reliability. — [Alibaba](https://electronics.alibaba.com/product/3d-realsense-camera)
- **Orbbec Femto Bolt (ToF):**
  - Specs: 1 MP ToF depth, 120° FOV (WFOV 120° × 120°; NFOV 75° × 65°), 0.25-5.46 m depending on mode, 850 nm; RGB 3840×2160 at 80° × 51°. — [Orbbec Femto Bolt datasheet](https://www.orbbec.com/wp-content/uploads/2023/08/ORBBEC_Datasheet_Femto-Bolt-0816-v01.pdf); [RobotShop UK](https://uk.robotshop.com/products/orbbec-femto-bolt-3d-vision-device)
  - Prices: £443.08 incl. tax at RobotShop UK; US$1,167.99 (sold out) at Openelab; ₹69,920 "includes GST and import duties" at Tanotis, India. — [Openelab](https://openelab.com/products/orbbec-femto-bolt-tof-camera); [Tanotis](https://www.tanotis.com/collections/3d-printers-accessories/products/orbbec-femto-bolt-depth-camera)
- **Orbbec Gemini 335 (stereo):**
  - Price: US$264 at the Orbbec store; US$304 at RobotShop. — [Orbbec store](https://store.orbbec.com/products/gemini-335); [RobotShop](https://www.robotshop.com/products/orbbec-gemini-335-camera)
  - Specs: depth FOV 90° × 65°, RGB 86° × 55°, range 0.10-20 m+ with optimal 0.26-3 m. — [Orbbec Gemini 335](https://orbbec.com/products/stereo-vision-camera/gemini-335)
  - The Gemini 335L variant (95 mm baseline, IP65, optimal 0.5-6 m) is US$413. — [RobotShop 335L](https://www.robotshop.com/products/orbbec-gemini-335l-camera)
- **Luxonis:**
  - OAK-D Lite: US$269.00 "VAT incl." in the Luxonis store; 4 TOPS of on-device processing, 13 MP central RGB. — [Luxonis store](https://checkout.luxonis.com/products/oak-d-lite-1)
  - OAK-D Pro: US$536.25; active stereo, 7.5 cm baseline, ideal range about 0.8-12 m, minimum depth 20-80 cm, DFOV 89.5° (80° × 55°). — [Knox Labs](https://www.knoxlabs.com/products/luxonis-oak-d-pro-depth-camera)
- **Camera behind two-way glass:**
  - Results are mixed. Some coatings block IR, and some mirrors work with a camera while others do not. One builder reports a PiCam behind the glass "works perfectly". — [MagicMirror forum post 18385](https://forum.magicmirror.builders/post/18385); [MagicMirror forum topic 2143](https://forum.magicmirror.builders/topic/2143/using-the-raspberry-pi-camera-to-see-through-the-mirror/19?page=1)
  - An 11%-transparency glass "blocks almost all of the light", and a shroud helps. — [TwoWayMirrors](https://www.twowaymirrors.com/hide-camera-behind-mirror/)

### Inferences
- **FOV needed (my geometry; framing a 2.0 m tall zone):**

| Distance | Camera at 1.0 m (mid) | At 1.6 m (eye level) | At 1.9 m (top bezel) | Horizontal for 1.0 m width |
|---|---|---|---|---|
| 1.0 m | 90.0° | 79.8° (tilt 18° down) | 68.0° (tilt 28°) | 53.1° |
| 1.5 m | 67.4° | 61.8° (tilt 16°) | 55.5° (tilt 24°) | 36.9° |
| 2.0 m | 53.1° | 50.0° (tilt 14°) | 46.4° (tilt 20°) | 28.1° |

- **Coverage at 1.5 m with the camera rotated 90° (my calculation):**
  - Pi Cam 3 Wide: 3.70 × 1.99 m.
  - C920 (about 70.4° × 43.3°, derived from 78° diagonal at 16:9): 2.12 × 1.19 m, which is tight.
  - Brio at 90°: 2.61 × 1.47 m.
  - D435/D455 depth: 2.85 × 1.66 m.
  - Gemini 335 depth: 3.00 × 1.91 m.
  - OAK-D Pro: 2.52 × 1.56 m.
  - Femto Bolt RGB: 2.52 × 1.43 m.
  - All except the C920 leave comfortable margins.
- **Placement:**
  - **Eye level behind the glass** gives the most mirror-like perspective. It loses 63-80% of the light through the glass (T = 20-37%) and risks display glare into the lens. Use a shroud, or cut a small clear window or hole in the mirror coating (common practice, but unsourced). It also puts the camera in front of the display area, which a portrait 55" panel covers from about 0.65-1.87 m.
  - **Top bezel** is easy and clean, but it needs a downward tilt and perspective correction (MemoMi's approach), and it still under-sees the feet when the user is close.
- **Recommendation:** an RGB-only Pi Cam 3 Wide or a USB UVC camera for the prototype. Add an Orbbec Gemini 335 (US$264; optimal 0.26-3 m, which matches the 1-2 m use zone) if depth-based body measurement or occlusion is needed. The Femto Bolt is better for measurement but about 4× more expensive in India.
- **Compatibility caution (unverified background, check before buying):** the Pi Camera Module 3 (IMX708) is natively supported on Raspberry Pi. Jetson JetPack support for IMX708 may need third-party drivers, so a USB camera or a Jetson-supported MIPI sensor is the safer choice with Jetson.

### Gaps
- No Indian prices were found for the Pi Camera Module 3 Wide, RealSense, Gemini 335 or OAK-D.
- No official RealSense US list prices for 2025-2026 were found (the realsenseai.com store was not reachable).
- OAK-D Lite FOV and depth range were not found.
- The Cognex-RealSense deal is unverified.

---

## 8. Compute options: specs, AI performance, power, prices (INR and USD)

### Takeaway
The **Jetson Orin Nano Super Developer Kit** is the best prototype fit: US$249 at launch, 67 TOPS sparse (about 33 TOPS dense), up to 25 W, and about ₹30,000-32,500 at ThinkRobotics. But **NVIDIA raised Jetson module and devkit prices by up to 101% in July 2026**: the Orin Nano 8GB module went from US$299 to US$399 at 1KU+.

Alternatives:
- **Raspberry Pi 5 + AI HAT+:** 26 TOPS (US$110), or AI HAT+ 2 at 40 TOPS INT4 with 8 GB onboard (US$130, Jan 2026). Cheap and low-power, but Pi 5 prices have risen sharply in the 2025-26 DRAM crunch (16GB: US$120, then US$145 in Dec 2025, then US$205 in Feb 2026).
- **RK3588 boards:** 6 TOPS NPU, under 10 W. Rock 5B 8GB costs about ₹12,200; Orange Pi 5 Plus 16GB about ₹26,000 on IndiaMART.
- **Mac mini M4:** ₹59,900, 16-core Neural Engine, 4-65 W.
- **RTX 4060/5060 mini PC:** only needed for heavy on-device generative try-on. The GPU alone costs ₹23-42k, and a whole PC draws far more power.

### Cited Findings
**NVIDIA Jetson Orin Nano Super Developer Kit**
- Announced 17 Dec 2024 at US$249, versus US$499 and 40 TOPS for the earlier kit. Rated 67 TOPS, which some outlets say is sparse, with a dense figure of 33 TOPS. It has 1,024 CUDA cores, 32 Tensor cores, 102 GB/s memory bandwidth and a 1.7 GHz CPU. Maximum performance needs the 25 W mode. It is the same hardware as the original Orin Nano, upgraded via JetPack. — [Phoronix, 17 Dec 2024](https://www.phoronix.com/news/NVIDIA-Jetson-Orin-Nano-Super); [Tom's Hardware](https://tomshardware.com/tech-industry/artificial-intelligence/nvidia-launches-new-usd249-ai-development-board-that-does-67-tops); [Gigazine](https://gigazine.net/gsc_news/en/20241218-nvidia-jetson-orin-nano-super); [InfoQ](https://www.infoq.com/news/2024/12/nvidia-jetson-ai-supercomputer)

**India prices, ThinkRobotics (undated snapshots, may predate the July 2026 hike)**
- Orin Nano Super Dev Kit: ₹29,999.99 (regular ₹32,999.99); ₹30,999.99 (sold out); ₹32,499.99. — [ThinkRobotics Jetson collection](https://thinkrobotics.com/collections/buy-nvidia-jetson-developer-kits-online); [ThinkRobotics home](https://thinkrobotics.com)
- "Made in India" Deployment Kit (Waveshare carrier, NVMe, Wi-Fi): ₹46,999-48,749. — [ThinkRobotics blog](https://thinkrobotics.com/blogs/product-reviews-buying-guides/nvidia-jetson-orin-super-nano-deployment-kit-made-in-india-everything-in-one-box-ready-to-deploy)

**July 2026 Jetson price increase**
- CNX Software (22 Jul 2026): NVIDIA raised Jetson module and devkit prices "by up to 101%", with new prices posted in the NVIDIA developer FAQ. The figures it reports:
  - Orin Nano 8GB module, 1KU+: US$299 to US$399.
  - Orin Nano 4GB module: US$349, up from US$199.
  - Orin NX 8GB: US$649.
  - [CNX Software, 22 Jul 2026](https://www.cnx-software.com/2026/07/22/nvidia-increases-the-price-of-jetson-modules-and-devkits-by-up-to-101/)

**Larger Jetsons**
- 2022 launch pricing at 1KU: Orin NX 16GB US$599; AGX Orin 64GB module US$1,599 (275 TOPS); AGX Orin devkit US$1,999. — [CNX Software, 22 Mar 2022](https://www.cnx-software.com/2022/03/22/nvidia-launches-jetson-agx-orin-developer-kit-orin-nx-modules-and-isaac-nova-orin-amr-platform/)
- A 2026 review still lists the AGX Orin 64GB devkit at US$1,999 and 275 TOPS. — [ThinkRobotics AGX Orin review](https://thinkrobotics.com/ar/blogs/product-reviews-buying-guides/nvidia-jetson-agx-orin-developer-kit-64gb-review-275-tops-in-a-110mm-cube)
- Orin NX reaches "up to 117 TOPS / 157 TOPS after upgrading to the SUPER version". Waveshare lists the Orin NX 16GB module at US$889.99 and US$1,279.99 on two SKU pages, which conflict. — [Waveshare Orin NX](https://www.waveshare.com/jetson-orin-nx.htm?sku=24056)

**Raspberry Pi 5 pricing in the DRAM crunch**
- Dec 2025: the 16GB rose from US$120 to US$145, and a US$45 1GB Pi 5 launched. — [The Register, 1 Dec 2025](https://www.theregister.com/2025/12/01/raspberry_pi_5_1gb/)
- Feb 2026: the 16GB reached US$205, "70% more than before the shortage", with Raspberry Pi saying "the cost of some parts has more than doubled over the last quarter". — [Tom's Hardware](https://www.tomshardware.com/raspberry-pi/raspberry-pi-5-price-increases-drastically-as-ai-shortage-bites-16gb-version-now-usd205-second-price-increase-in-three-months-over-70-percent-more-expensive-than-original-msrp); [Notebookcheck](https://www.notebookcheck.net/Raspberry-Pi-5-now-costs-up-to-205-due-to-RAM-crisis.1218213.0.html)
- PCWorld (Apr 2026) reports the 16GB rising "by $100 to $220". This conflicts with the US$205 figure and is unverified. — [PCWorld](https://www.pcworld.com/article/3106353/raspberry-pi-5-is-getting-a-100-price-hike-thanks-to-ram-shortage.html)
- Coverage notes CEO Eben Upton expects to reverse the increases when memory prices ease. — [Hackster.io](https://www.hackster.io/news/memory-pricing-leads-to-a-5-25-price-hike-for-the-raspberry-pi-5-single-board-computer-family-26f2aee18ce5); [Astute Group](https://www.astutegroup.com/news/memory-shortages/raspberry-pi-price-rises-as-memory-crisis-deepens-but-hope-flickers-for-ddr5-ram-market/)
- India:
  - KSP Electronics lists the Pi 5 16GB at ₹34,191 incl. GST, out of stock. — [KSP Electronics](https://kspelectronics.in/product-category/raspberry-pi/raspberry-pi-boards/raspberry-pi-5-boards/)
  - Smartprix showed ₹15,439 in Mar 2025, which is outdated. — [Smartprix](https://www.smartprix.com/raspberry_pi/price-below_18000)
  - A ThinkRobotics guide dated Feb 2026 gives the 4GB at ₹5,500-6,200, which looks pre-hike. — [ThinkRobotics Pi 5 India guide](https://thinkrobotics.com/blogs/product-reviews-buying-guides/raspberry-pi-5-price-india-complete-cost-analysis-and-buying-guide)

**Raspberry Pi AI accelerators**
- AI HAT+ launch prices: 26 TOPS (Hailo-8) US$110; 13 TOPS (Hailo-8L) US$70. The Pi Hut sells them at £105.60 and £67.20 incl. VAT. — [Tom's Hardware](https://tomshardware.com/raspberry-pi/raspberry-pi-release-higher-performance-ai-hat-13-and-26-tops-variants); [The Pi Hut](https://thepihut.com/collections/raspberry-pi/products/raspberry-pi-ai-hat-plus)
- AI HAT+ 2: Hailo-10H, 40 TOPS INT4, 8 GB LPDDR4X-4267 onboard, PCIe to the Pi 5. Official price US$130; release date 15 Jan 2026 per a Japanese retailer; 1,599 SEK at Electrokit. — [Tecnoblog](https://tecnoblog.net/noticias/raspberry-pi-anuncia-placa-ai-hat-2-com-40-tops-para-ia-preco-e-alto/); [Switch Science](https://www.switch-science.com/products/10916); [Electrokit](https://www.electrokit.com/en/raspberry-pi-ai-hat2)

**RK3588 boards**
- Orange Pi 5 Plus 16GB:
  - Specs: NPU 6 TOPS (INT4/INT8/INT16/FP16); CPU 4× Cortex-A76 at 2.4 GHz plus 4× A55 at 1.8 GHz; launched at 999 yuan for the 16GB. — [IT之家](https://www.ithome.com/0/692/295.htm)
  - India: ₹25,999 on IndiaMART (Ahmedabad seller); ₹43,236 on Ubuy, excluding shipping and customs. — [IndiaMART](https://m.indiamart.com/proddetail/orange-pi-5-plus-single-board-computer-2855512731097.html); [Ubuy India](https://www.ubuy.co.in/product/F4X7W8YZY-orange-pi-5-plus-16gb-rockchip-rk3588-8-core-64-bit-single-board-computer-2-4ghz-frequency-open-source-development-board-run-orange-pi-os-android)
  - US: 52Pi bundle with case, PSU and fan at US$232.88; Newegg US$415.99 with PSU. — [52Pi](https://52pi.com/zh/products/orange-pi-5-plus-16gb-lpddr4-4x-rockchip-rk3588-8-core-64-bit-single-board-computer-with-emmc-socket-opi-5-plus-metal-case-official-orange-pi-5v-4a-power-supply-40-mm-fan-for-orange-pi-5); [Newegg](https://www.newegg.com/p/3C6-03VM-01V97)
- Radxa ROCK 5B 8GB: ₹10,321.19 plus 18% GST (about ₹12,179) at Hubtronics; ROCK 5B+ ₹12,099.99 at ThinkRobotics (pre-order or sold out). — [Hubtronics](https://hubtronics.in/radxa/rs119-d8?page=5); [ThinkRobotics ROCK 5B+](https://thinkrobotics.com/products/radxa-rock-5b-1)
- ROCK 5B power, one user's wall measurement: about 3 W idle, "not exceeding 10W" under the heaviest benchmarks. — [Radxa forum](https://forum.radxa.com/t/rock-5b-debug-party-invitation/10483/41)

**Apple Mac mini M4**
- India launch (Oct 2024): ₹59,900 for 10-core CPU/GPU, 16 GB and 256 GB; ₹79,900 and ₹99,900 for 512 GB configurations. It has a 16-core Neural Engine. — [ETV Bharat](https://etvbharat.com/en/!technology/apple-mac-mini-2024-india-launch-price-specifications-enn24103002609); [MobiGyaan](https://www.mobigyaan.com/apple-mac-mini-m4-pro-2024-india)
- A forum post cites 38 TOPS and a ₹55,900 bank-offer price (Mar 2026). — [TechEnclave](https://techenclave.com/t/mac-mini-in-march-2026-m5-was-a-no-show-and-here-is-what-that-actually-means/418835)
- Power: Apple lists 4 W idle and 65 W maximum (16 GB / 256 GB model). ServeTheHome measured 4-6 W idle and 40-45 W "normal maximum"; Jeff Geerling measured 3-4 W idle. — [AppleInsider](https://appleinsider.com/articles/25/05/04/its-tough-but-you-can-hack-a-m4-mac-mini-to-get-power-over-usb-c); [ServeTheHome](https://servethehome.com/the-apple-mac-mini-m4-sets-the-mini-computer-standard/3); [Jeff Geerling](https://jeffgeerling.com/node/3419)

**RTX-class GPUs in India**
- RTX 4060: about ₹23,000-27,000 (May 2026 guide), or ₹34,000 "indicative" (a conflicting source). — [GetPC RTX 5060 guide](https://getpc.co.in/parts/gpu/rtx-5060); [GetPC 4060 vs 5060](https://getpc.co.in/compare/rtx-5060-8gb-vs-rtx-4060)
- RTX 5060: low of ₹36,999 on 6 Jul 2026 (3-month median ₹38,499). — [GPUPrix](https://gpuprix.com/zh/india/gpus/geforce-rtx-5060)
- RTX 5060 laptops: from ₹1,25,990, with 2026 RAM shortages pushing prices up. — [GamingNation](https://gamingnation.in/best-rtx-5060-gaming-laptop-india/)

### Inferences
- **Match compute to the try-on pipeline (the software choice is covered by other researchers):**
  - **Real-time AR overlay** (pose, segmentation, 2D/3D garment warp at 30 fps): Jetson Orin Nano Super is a comfortable fit. Pi 5 + AI HAT+ or HAT+ 2 is feasible for pose and segmentation but weak for garment rendering. RK3588 is marginal.
  - **Generative (diffusion) photo try-on:** typically needs a large-VRAM desktop GPU or a cloud API. An on-device RTX 4060/5060 PC raises power, heat and cost sharply. A hybrid (local real-time preview plus a cloud "final look" render) is likely the practical home-product architecture. This is an inference; model VRAM needs were not researched here.
- **Price volatility:** DRAM-driven increases in 2025-26 hit both Raspberry Pi (16GB up 70%+) and NVIDIA Jetson (up to 101%, July 2026). Re-quote compute immediately before buying. Indian listings may lag the US increases.
- **India one-off import penalty:** the same item costs 1.35-2.2× more when bought one-off in India through importers. The Femto Bolt is ₹69,920 versus £443 at RobotShop UK (about 1.35× at 1.33 US$/£ and ₹88/$). The QM55C is about 2.2× US street. The Orange Pi 5 Plus via Ubuy (₹43,236 before customs) costs about 1.7× the local IndiaMART stock price.

### Gaps
- **Not found because of the search budget:**
  - The post-July-2026 price of the Orin Nano Super Developer Kit.
  - Current Robu.in and Evelta prices (robu.in was not reachable).
  - Pi 5 4GB and 8GB prices after the Feb 2026 hike.
  - Indian prices for the AI HAT+ and AI HAT+ 2.
  - RTX mini-PC system prices.
  - Mac mini M4 US price.
- **Power figures not sourced:**
  - Raspberry Pi 5 + HAT. Unverified background: Pi 5 about 3-12 W, official 27 W PSU; the AI HAT+ adds a few watts.
  - RTX 4060/5060 desktop GPU board power. Unverified background: about 115 W and about 145 W TGP; a full mini PC about 150-250 W under load.
- **Jetson AGX Thor and other 2025-26 Jetson SKUs** were not researched.

---

## 9. Other parts: presence sensors, audio, high-CRI lighting, colour calibration, frame, cooling, mounting

### Takeaway
None of these parts could be price-checked before the shared search budget ran out. The engineering requirements below are reasoned from the rest of the research. Prices are listed only as unverified background placeholders in Gaps.

### Cited Findings
- No sourced findings were obtained for this section (search budget exhausted). The relevant cited constraints come from other sections:
  - Front lighting directly raises reflection brightness (L = ρE/π). — [Wikipedia: Luminance](https://en.wikipedia.org/wiki/Luminance)
  - Backlight bleed is hidden only when the front is brighter than the display behind. — [MagicMirror forum](https://forum.magicmirror.builders/post/45961)

### Inferences
- **Presence sensing:**
  - A PIR (HC-SR501) detects motion only and misses a still person posing.
  - A 24 GHz mmWave sensor (HLK-LD2410 family) detects stationary presence and ranges, and works through a plastic or wood frame. Unverified: most mmWave sensors need a non-metal window, so a metal frame or the mirror coating may block them.
  - Use the camera itself for fine presence once the system is awake, and the mmWave sensor for wake/sleep to save power.
- **High-CRI lighting:**
  - Use CRI ≥90 (ideally ≥95, with R9 stated) LED strips at 4000-5000 K, with a diffuser, on the left and right sides of the mirror for even facial and body lighting, plus a dimmable driver.
  - Dimming is necessary because the lighting must drop during try-on so the display dominates (Section 2).
- **Colour calibration:**
  - Photograph a ColorChecker-type card under the mirror's own LEDs to build a camera colour-correction matrix.
  - Calibrate the display (or at least set a fixed picture mode and white point), because the product judges colour combinations.
  - Without both steps the "digital mirror" will shift garment colours.
- **Audio:**
  - A USB far-field microphone array (2-4 mics with on-board AEC/beamforming) for voice control at 1-2 m, plus small full-range speakers behind grilles in the frame.
  - Most TVs' own speakers face down or back and will be muffled inside an enclosure.
- **Frame, enclosure and cooling:**
  - Use an aluminium extrusion or plywood/MDF frame with a rear service panel.
  - Add a vent path at the bottom (intake) and top (exhaust) behind the TV. About 100-200 W of heat is dissipated inside (Section 10).
  - Add 1-2 quiet 120 mm fans with thermal control, and keep the compute board outside the TV's hot exhaust plume.
- **Mounting and anti-tip:**
  - The assembly is about 35-50 kg (Section 4), so use a wall-mounted cleat or a VESA wall mount with anchors rated for the wall type.
  - A freestanding version needs a weighted base plus an anti-tip strap or bracket to the wall.

### Gaps
- **Unverified background placeholders (re-check on Robu.in, Amazon.in, ThinkRobotics or Evelta before use):**
  - HC-SR501 PIR: about ₹50-120.
  - HLK-LD2410 / LD2410B / LD2410C mmWave: about ₹250-600.
  - USB 4-mic array (e.g. a ReSpeaker-class XMOS board): about US$40-80.
  - A pair of small speakers plus an amplifier: about ₹1,000-3,000.
  - CRI 90-95+ 24 V COB/SMD strip at 4000-5000 K: about ₹300-1,200 per metre, plus a 24 V PSU and dimmer at about ₹800-2,000.
  - Calibrite ColorChecker Classic: about US$90-110 (Passport Photo 2: about US$120-150).
  - Aluminium extrusion frame materials: about ₹3,000-10,000.
  - Fans: about ₹500-1,500.
  - TV wall mount: about ₹1,000-3,000.
- No sourced data on anti-tip standards or wall-anchor ratings for Indian brick or drywall.

---

## 10. Power: component draw, total, and whether battery operation is realistic

### Takeaway
A Jetson plus 55" TV mirror draws about **120-185 W** while running: the TV about 80-120 W, Jetson 15-25 W, LEDs about 20-30 W, and about 5-10 W for the rest. A Pi 5 plus 43" build draws about 90-135 W. A signage panel plus RTX PC build draws about 275-440 W. Three hours of use needs about **360-555 Wh** (about 425-650 Wh including inverter losses) for the Jetson build, and about 1-1.5 kWh for the GPU build. Battery operation is possible with a 0.5-1 kWh portable power station, but it adds cost, weight and fire risk for no user benefit in a home dressing area. Mains power, with optional small-UPS protection for the compute, is the practical design.

### Cited Findings
- **TV:** 43" 4K EU fiche: 54 W on-mode, 0.5 W standby. — [BT energy fiche (Toshiba 43UL2063DB)](https://m.businessdirect.bt.com/images/EnergyComplianceInfo/FY5V/EnergyFicheURL/631257_fiche-27924.pdf)
- **TV:** 55" 4K HDR: at least 70-90 W. — [Webwoordenboek](https://webwoordenboek.nl/kenniscentrum/hoeveel-watt-is-een-4k-tv)
- **Jetson Orin Nano Super:** 25 W for maximum performance. — [Tom's Hardware](https://tomshardware.com/tech-industry/artificial-intelligence/nvidia-launches-new-usd249-ai-development-board-that-does-67-tops)
- **Mac mini M4:** 4 W idle and 65 W maximum (Apple, via AppleInsider); 40-45 W normal maximum measured. — [AppleInsider](https://appleinsider.com/articles/25/05/04/its-tough-but-you-can-hack-a-m4-mac-mini-to-get-power-over-usb-c); [ServeTheHome](https://servethehome.com/the-apple-mac-mini-m4-sets-the-mini-computer-standard/3)
- **RK3588 (ROCK 5B):** about 3 W idle, 10 W or less under load (one user's measurement). — [Radxa forum](https://forum.radxa.com/t/rock-5b-debug-party-invitation/10483/41)

### Inferences
- **Energy budget (my arithmetic; LED, misc, Pi and PC figures are assumptions marked in Gaps):**

| Build | Running power | 2 h | 3 h | 4 h | 3 h incl. 85% inverter efficiency |
|---|---|---|---|---|---|
| Budget: 43" TV + Pi 5/AI HAT + LEDs + misc | ~89-135 W | 178-270 Wh | 267-405 Wh | 356-540 Wh | 314-476 Wh |
| Jetson: 55" TV + Orin Nano Super + LEDs + misc | ~120-185 W | 240-370 Wh | 360-555 Wh | 480-740 Wh | 424-653 Wh |
| High-end: 55" 500-nit signage + RTX mini PC + LEDs | ~275-440 W | 550-880 Wh | 825-1,320 Wh | 1,100-1,760 Wh | 971-1,553 Wh |

- **Ways to cut energy:**
  1. Sleep the display and LEDs via the mmWave sensor. With the TV at 0.5 W standby, idle draw is dominated by the compute (Jetson at idle a few watts, unverified).
  2. Dim the LEDs except during try-on.
  3. Use a 43-50" panel.
- **Battery verdict:** a "few hours" of use needs a battery pack of roughly the size of a 0.5-1 kWh consumer power station, 6-12 kg. That weight is my rough figure, not sourced. Mains power is available in any dressing area, so battery operation only makes sense for a portable demo or kiosk unit.

### Gaps
- **No sourced power figures** for 500-700-nit signage panels (e.g. QM55C typical and maximum), the Pi 5 + AI HAT+, RTX mini PCs, LED strips, or portable power stations and their Indian prices. All were blocked by the search budget.
- **Unverified background placeholders:**
  - CRI 90+ 24 V strips: about 10-15 W/m, so 2 × 1.5 m is about 30-45 W at full brightness.
  - 55" 500-nit signage: about 100-150 W.
  - Li-ion pack energy density: about 150-250 Wh/kg at the cell level.

---

## 11. DIY references: MagicMirror², published smart-mirror build guides, open-source try-on mirror builds

### Takeaway
The MagicMirror² community forum supplies most of the practical, experience-based guidance on glass transmission, backlight bleed and cameras behind glass. TwoWayMirrors.com publishes smart-mirror parts lists and system pricing. No open-source *virtual try-on* mirror build was found within the budget. The try-on mirror is effectively a new combination of a MagicMirror-style frame, a digital-mirror camera pipeline and a try-on model.

### Cited Findings
- **MagicMirror forum guidance:**
  - Glass transmission by room type (4-10%, 12-20%, 30-50%). — [MagicMirror forum](https://forum.magicmirror.builders/post/48954)
  - Light in front should exceed the monitor's brightness to hide bleed. — [MagicMirror forum](https://forum.magicmirror.builders/post/45961)
  - Pi cameras behind two-way glass work with some coatings and not others. — [MagicMirror forum topic 2143](https://forum.magicmirror.builders/topic/2143/using-the-raspberry-pi-camera-to-see-through-the-mirror/19?page=1)
- **TwoWayMirrors.com** offers smart-mirror PCAP foil (US$1,976.87 for 55") with "a complete parts list and step-by-step guide, as well as pricing for complete systems". — [TwoWayMirrors PCAP foil](https://www.twowaymirrors.com/pcap-foil/)
- **Pilkington and Visualplanet** demonstrated an integrated MirroView + touchfoil smart mirror (ISE 2017). — [Pilkington news](https://my.pilkington.com/en/news-insights/latest/nsg-group-and-visualplanet-to-exhibit-integrated-smart-mirror-at-ise-2017)

### Inferences
- MagicMirror²-style builds are "information mirrors": text and widgets on a dark background behind low-transmission (about 12-20%) glass. That is the opposite of what try-on needs: high transmission and a full-screen bright video. Reuse their frame, mounting and glass-handling know-how, not their glass choice.

### Gaps
- **Not verified (search budget exhausted):** MagicMirror² project facts. Unverified background: open-source (MIT), Node.js/Electron, modular third-party "modules", started by Michael Teeuw around 2014, runs on Raspberry Pi.
- **Not found:**
  - Published build-cost breakdowns, such as typical Pi + monitor + two-way acrylic DIY builds.
  - Instructables-style guides with parts lists.
  - GitHub open-source virtual try-on mirror projects (e.g. Jetson/OpenCV/MediaPipe AR fitting rooms).
  - A follow-up search is needed for these.

---

## 12. Bill of materials: (A) one-off DIY prototype in India, (B) estimate at about 1,000 units, and import-duty notes

### Takeaway
- **(A) DIY prototype:** a digital-mirror build with a 55" TV, Jetson Orin Nano Super, C920s-class camera, MirroView-50/50-type glass and an imported IR frame comes to **about ₹1.07-1.69 lakh (about US$1,200-1,900)**. Without touch it is **about ₹0.87-1.32 lakh**.
- **Budget variant:** a 43" TV, Pi 5 + AI HAT+ and Pi Cam 3 Wide comes to **about ₹0.52-0.93 lakh**.
- **(B) Per unit at 1,000 units:** for the Jetson design, the bottom-up per-unit BOM plus assembly, freight and warranty estimate is **about US$940-1,590 (₹0.83-1.40 lakh)**. With RK3588- or Pi-class compute it is **about US$600-1,290**.
- **Biggest uncertainties:** display (open-cell vs signage), glass, and Jetson pricing after the July 2026 increase.

### Cited Findings
(Sourced unit prices used in the BOM; full citations in Sections 4-8.)
- **55" 4K TV:** ₹26,699 (Blaupunkt, Jun 2026), ₹28,499 (Hisense E6N, Amazon, undated), ₹30,399 (Acer V, Jun 2026), ₹33,999 (Vu GloQLED or NU QLED, May-Jul 2026). — [MySmartPrice](https://www.mysmartprice.com/electronics/pricelist/50-inch-led-tv-price-list-in-india.html); [PriceHistory](https://pricehistoryapp.com/product/hisense-139-cm-55-inches-e6n-series-4k-ultra-hd-smart-led-google-tv-black); [MagicDrop](https://magicdrop.in/drops/55-inch-qled-tv)
- **43" 4K TV:** ₹16,499 (Kenstar, Jul 2026), ₹21,999 (realme), ₹23,990 (Hisense 43A6K, Jun 2026). — [Smartprix](https://www.smartprix.com/tvs/kenstar-brand); [PriceBefore](https://www.pricebefore.com/realme-techlife-108-cm-43-inch-p1018574.html); [MySmartPrice](https://www.mysmartprice.com/electronics/hisense-43a6k-43-inch-uhd-smart-led-tv-msf612241)
- **Jetson Orin Nano Super Dev Kit:** ₹29,999.99-32,499.99 at ThinkRobotics (undated); US$249 at launch (Dec 2024). The module is US$399 at 1KU+ after the July 2026 increase. — [ThinkRobotics](https://thinkrobotics.com/collections/buy-nvidia-jetson-developer-kits-online); [CNX Software](https://www.cnx-software.com/2026/07/22/nvidia-increases-the-price-of-jetson-modules-and-devkits-by-up-to-101/)
- **Pi accelerators:** AI HAT+ 26 TOPS US$110; AI HAT+ 2 US$130. **Camera:** Pi Cam 3 Wide about US$32-35. — [Tom's Hardware](https://tomshardware.com/raspberry-pi/raspberry-pi-release-higher-performance-ai-hat-13-and-26-tops-variants); [Tecnoblog](https://tecnoblog.net/noticias/raspberry-pi-anuncia-placa-ai-hat-2-com-40-tops-para-ia-preco-e-alto/); [Elecena](https://elecena.pl/product/27036821/rss)
- **Logitech C920s (India):** ₹6,999-7,999. — [GetPC](https://getpc.co.in/parts/webcam/logitech-c920s)
- **Depth camera options:** Orbbec Gemini 335 US$264 (Orbbec store); Femto Bolt ₹69,920 (Tanotis, incl. GST and duty). — [Orbbec store](https://store.orbbec.com/products/gemini-335); [Tanotis](https://www.tanotis.com/collections/3d-printers-accessories/products/orbbec-femto-bolt-depth-camera)
- **55" IR frame:** US$51-164 (Alibaba, MOQ 10); US$160 (eBay); US$297.99 (Newegg). **55" PCAP foil:** US$1,976.87 (TwoWayMirrors). — [Alibaba](https://electronics.alibaba.com/product/ir-touch-screen-frame-overlay); [eBay](https://www.ebay.com/str/professionaltouchscreenstore); [Newegg](https://www.newegg.com/p/3C6-05G2-01AA3); [TwoWayMirrors](https://www.twowaymirrors.com/pcap-foil/)
- **Reflective / one-way glass in India:** ₹75-2,900/sq ft (IndiaMART). — [IndiaMART](https://m.indiamart.com/impcat/reflective-glass.html)
- **Signage alternative:** Samsung QM55C at US$1,260 (US) or ₹2,41,105 (India, incl. GST and duties). — [CompSource](https://www.compsource.com/buy/QM55C/389); [Tanotis](https://www.tanotis.com/collections/commercial-monitors-displays/products/samsung-qm55c-55-uhd-4k-commercial-monitor)
- **Indian retail benchmark:** smart mirrors with touch displays sell for about ₹30,000-80,000. — [StudioMatrx](https://www.studiomatrx.org/guides/smart-bathroom-mirror-india)

### Inferences
**(A1) Recommended DIY prototype: "digital mirror" on Jetson, 55" (INR, one-off, India)**

| Item | Choice | ₹ low | ₹ high | Basis |
|---|---|---|---|---|
| Display | 55" 4K consumer TV, portrait-mounted | 26,699 | 33,999 | Sourced (Jun-Jul 2026 listings) |
| Mirror glass | MirroView 50/50 / dielectric 6 mm, toughened, cut to ~1.8 × 0.75 m | 5,000 | 15,000 | **Assumption** (no MirroView price found; IndiaMART ₹75-2,900/sq ft × 14.5 sq ft = ₹1,090-42,000) |
| Compute | Jetson Orin Nano Super Dev Kit | 29,999 | 32,499 | Sourced (may predate July 2026 increase) |
| Storage | NVMe SSD 256-512 GB | 2,000 | 4,000 | Assumption |
| Camera | Logitech C920s (or Brio for 90° FOV) | 6,999 | 7,999 | Sourced (C920s) |
| Touch (optional) | 55" IR frame, imported | 19,712 | 36,714 | US$160-298 sourced × ₹88 × 1.4 (assumed duty and shipping) |
| Lighting | CRI 90-95, 4000-5000 K strips + 24 V PSU + dimmer | 2,000 | 5,000 | Assumption |
| Presence sensor | LD2410-class mmWave (+ optional PIR) | 100 | 600 | Assumption |
| Audio | USB mic array + small speakers/amp | 1,500 | 6,000 | Assumption |
| Frame and mounting | Al-extrusion or ply frame, fans, wall cleat / anti-tip | 5,000 | 15,000 | Assumption |
| Colour calibration | ColorChecker-type card | 8,000 | 12,000 | Assumption |
| **Total** | | **≈1,07,000** | **≈1,69,000** | ≈US$1,216-1,918 |
| Total without touch | | ≈87,300 | ≈1,32,100 | |

- **Optional add-on:** an Orbbec Gemini 335 depth camera (US$264 plus import, roughly ₹28-35k landed, assumed), or a Femto Bolt (₹69,920).

**(A2) Budget prototype: Pi 5, 43" (INR)**
- 43" 4K TV: ₹16,499-23,990 (sourced).
- Smaller two-way glass: ₹3,000-10,000 (assumption).
- Pi 5 8GB: ₹9,000-14,000 (assumption; post-hike Indian price not found).
- AI HAT+ 26 TOPS: about ₹10,600-13,600 (US$110 × ₹88 × 1.1-1.4, assumed landed).
- Pi Cam 3 Wide: about ₹3,400-4,300 (US$35 × 1.1-1.4).
- PSU, SD card, case and cooler: ₹2,000-3,500.
- LEDs: ₹2,000-5,000. Sensors: ₹100-600. Audio: ₹1,500-6,000. Frame and mount: ₹4,000-12,000.
- **Total ≈ ₹52,100-93,000 (≈US$590-1,060).** This build suits pose and segmentation overlays, not heavy garment rendering.

**(B) Indicative per-unit cost at about 1,000 units (USD, Jetson design)**

| Item | US$ low | US$ high | Basis |
|---|---|---|---|
| 55" 4K LCD open-cell/TV-grade module + driver board (or 500-nit panel at the high end) | 170 | 300 | **Assumption** (Indian retail 55" TVs cost ₹26.7-34k incl. GST, about US$300-390, so module cost must be below that; signage panel retail is US$1,260) |
| 6 mm toughened 50/50 or dielectric two-way glass, ~1.35 m² | 50 | 150 | Assumption |
| Jetson Orin Nano 8GB module (US$399 at 1KU+) + carrier/SSD/Wi-Fi | 459 | 519 | Module sourced (Jul 2026); carrier etc. assumed US$60-120 |
| Wide MIPI/USB camera module | 15 | 35 | Assumption (Pi Cam 3 Wide retail US$32-35) |
| 55" IR frame at volume | 50 | 90 | Assumption from Alibaba US$51-164 at MOQ 10 |
| High-CRI LED strips + driver | 10 | 25 | Assumption |
| mmWave sensor + mic array + speakers | 15 | 40 | Assumption |
| PSU, cabling, fans | 20 | 40 | Assumption |
| Frame/enclosure, mount, anti-tip kit | 60 | 150 | Assumption |
| Assembly, test, packaging | 40 | 90 | Assumption |
| Freight, duties, warranty reserve | 50 | 150 | Assumption |
| **Total per unit** | **≈939** | **≈1,589** | ≈₹82,600-1,39,800 |

- **Compute is the largest line.** The Jetson module plus carrier is about 30-50% of the BOM. Replacing it with an RK3588 SoM or a Pi CM5 + Hailo, at an assumed US$120-220, gives **≈US$600-1,290** per unit, at the cost of AI headroom.
- **Retail price implication:** at about US$940-1,590 BOM, a consumer price under ₹1 lakh is unrealistic with Jetson-class compute. The Indian benchmark of ₹30-80k for touch smart mirrors suggests targeting RK3588/Hailo-class compute plus cloud inference for heavy generative try-on. This is an inference, and margin structure was not researched.
- **Import-duty note (inference from price ratios):** one-off imports through Indian resellers cost 1.35-2.2× overseas street prices (Femto Bolt, QM55C and Orange Pi examples, Section 8). For volume, local TV-panel sourcing (India has domestic TV assembly) and importing only modules (Jetson/Hailo, touch frames) on proper HSN codes would be the cost lever. Actual BCD/IGST rates were not verified.

### Gaps
- **Indian customs duty rates (BCD + IGST)** were not researched (search budget exhausted): Jetson modules and dev kits, SBCs, cameras, IR touch frames, open-cell panels and signage displays. Unverified background: IGST is generally 18% on electronics, and open-cell TV panels have had concessional BCD in recent Indian budgets. Verify on CBIC/ICEGATE before costing.
- **Unverified background:** GST on TVs over 32" was reportedly cut from 28% to 18% in the Sept 2025 GST rationalisation.
- **No supplier quotes at volume** for open-cell panels, MirroView/dielectric glass, PCAP foil, frames or assembly. Every "Assumption" row should be replaced with RFQ data.
- **Post-July-2026 Jetson devkit pricing** in India and the US was not found.
- All INR/USD conversions assume ₹88/US$, which is unsourced.

### Meta
2024-09-25 13:35
**Tags:** [[color_theory]] [[color_gamut_spaces_systems]]
**Status:** #completed  

### The CIE XYZ Color Space
- Developed to be independent of devices or other means of emission or reproduction of color.
- Based on colorimetry experiments by William David Wright (1929) and John Guild (1931).
- The subjects in these experiments developed tristimulus values by visually matching a test color against the RGB primary colors.
- Due to the distribution of cones in the retina, tristimulus values are developed on a subjects field of view.
- CIE established a color-mapping function called the **standard (colorimetric) observer** to remove this variation.
- This is based on the assumption that color-sensitive cones are located within **2°** of the arc of the fovea inside the retina of the eye.
- Instead of using direct RGB data from the human subject colorimetry studies, CIE developed a mathematical formula in order to convert RGB data to a system of only positive integers.
- These were noted as `XYZ`.
- They do NOT directly correspond to the RGB values of the Wright and Guild colorimetry studies.

### CIE x-y Chromaticity Diagram
- CIE also derived a two-dimensional equivalent to the CIE XYZ color space called the **CIE x-y chromaticity diagram**.
- CIE established a new set of chromacity coordinates coordinates called `x`, `y`, and `z` exhibiting the property that `x + y + z = 1`.
- The coordinate `z` is not displayed in the CIE x-y chromaticity diagram, but can be derived from the `x + y + z = 1` relationship.
- The two-dimensional visualization is a result of developing a chart with `x` and `y` as its axes to plot points that indicate chromaticity.
- It working with the CIE XYZ color space, the tristimulus values are always indicated in upper case as `X`, `Y`, and `Z`, and the chromaticity coordinates are always noted in lower case as `x`, `y`, and `z`.

![[CIE_x-y_chromaticity_diagram.png]]

- Plotting the `x` and `y` values of spectral colors ranging from 400 to 700 nm on the x-y chromaticity diagram results in a horseshoe-shaped curve.
- The edge line of this diagram is called the **spectral locus** – pure monochromatic light measured by wavelength in nanometers.
- These are the most saturated colors of the horseshoe.
- The non-spectral Magenta `#f0f` or Purple-Red mixtures fall along the straight line joining the 400 nm point to the 700 nm point of the horseshoe.
- This line is often termed the **Line of Purples**.
- The colors of this line are also fully saturated and are made by mixing Red and Blue colors.
- All visible colors fall within the resulting closed horseshoe curve.
- Pale and unsaturated colors lie nearer the center of the diagram.
- The central point of `x = 1/3` and `y = 1/3` is defined as the **achromatic point** where visually perceived White is located.
- If we define two colors in the chromaticity diagram as individual end points and place a line between them, the colors along the resulting line are produced via combinations of the two color end points.
- The Line of Purples is one demonstration of this characteristic.

#### Shortcomings
- One of the shortcomings of the CIE x-y chromaticity diagram is that colors of equal amounts of difference appear further apart in the Green region of the visualization than they do in the Red or violet part.
- It is frequently noted that Green takes up a disproportionately large fraction of the diagram compared to other colors.
- To address this issue of nonuniform scaling, CIE adopted two uniform diagrams, the [CIE LUV]([[cie_luv_color_space]]) and the [CIE LAB]([[cie_lab_color_space]]), as specifications in 1976.
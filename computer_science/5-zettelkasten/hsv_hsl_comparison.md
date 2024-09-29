### Meta
2024-09-26 12:49
**Tags:** [[color_gamut]] [[hsv_hsl_color_spaces]] [[geometry_of_hsv_hsl]]
**Status:** #completed  

### Comparison of HSV and HSL Color Spaces
- The **HSV** color space is represented as a *single cone*.
- The **HSL** color space is depicted as a double cone.
- For both geometric shapes, the central vertical axis represents an achromatic or a neutral axis with Black at the bottom at a *value* of `0` in HSV and a *lightness* of `0` in HSL.
- White is at the top of the central axis with *value* `1` in HSV and *lightness* `0` in HSL.
- The hue circle of colors is positioned in both color spaces around the edge of the geometric shape at *saturation* `1`.
- In HSV, the hue circle is positioned at the top of the cone with a *value* `1`.
- In HSL, the hue circle is positioned in the middle of the double cone with *lightness* `0.5`.
- This position results in some differences in the mixing of the pure colors on the hue circle’s outer edge.
- In HSV, mixing pure colors with White reduces saturation, yielding *tints*, while mixing pure colors with Black leaves saturation scales unchanged, resulting in *shades*.
- With HSL, both *tints* and *shades* have *full saturation*, while *tones*, mixtures of both Black and White, have saturation levels less than `1`.
- A key advantage of HSV is the conceptual simplicity.
- As noted previously, the *saturation* attribute in HSV corresponds to *tinting* with *desaturated colors* having increasing total intensity. This is a limitation of the HSV color space.
- As a result, the **CSS** standard for Web content development supports **RGB** and **HSL**, but not HSV.
- HSV and HSL are computationally efficient color spaces for color selection while creating digital content.
- A key disadvantage of the HSV and HSL color spaces is in regard to addressing the complexity of color appearance such as perceptual uniformity.
- Bot color spaces are not absolute color spaces such as the CIE color spaces or the Munsell color order system.
- HSV and HSL are defined purely with reference to a given RGB space.
- Due to the abundance of commonly applied RGB color spaces, precise specification of a color involves noting the HSV or HSL attributes as well as the characteristics of the reference RGB color space and the associated gamut correction in use.
- Fundamentally, HSV and HSL color spaces trade off perceptual uniformity for computational speed, optimal for many digital content creation situations, such as interactive visualization, real-time virtual environments, or computer game development, where such computational speed is optimal.
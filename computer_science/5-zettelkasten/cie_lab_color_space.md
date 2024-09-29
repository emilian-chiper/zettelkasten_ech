### Meta
2024-09-25 18:49
**Tags:** [[color_theory]] [[color_gamut_spaces_systems]]
**Status:** #completed 

### CIE LAB
- Is a **three-dimensional opponent** color space that accurately represents perceptual distances between different colors.
- According to opponent theory, in the brain, retinal color stimuli become translated into distinctions between the following:
	(1) light and dark (White and Black),
	(2) Red and Green, and
	(3) Yellow and Blue.
- CIE LAB indicates that in these three components one axis (`L*`) plots the lightness or luminance from White to Black, a second axis (`a*`) plots values between Red and Green, and a third axis (`b*`) plots values between Yellow and Blue.
- These color axes are determined by the concept that a given color cannot simultaneously be Red and Green, or Yellow and Blue, because the colors are in opposition.
- On the `a*` axis, positive values represent amounts of Red `#f00`, while negative values represent amounts of Yellow `#ff0`.
- On the `b*` axis, positive values represent amounts of Yellow `#ff0`, whereas negative values represent amounts of Blue `#00f`.
- Individual colors are represented according to their corresponding positions on all three axes.

![[CIE_LAB_color_space_3d_representation.png]]

- CIE `L*a*b*` is a device-independent color space that includes all perceivable colors and its gut exceeds those of the RGB and CMYK color models.
- This allows it to serve as an intermediary color space where values from a particular gamut are re-encoded as CIE `L*a*b` values and other devices can convert them into their own specific gamut.
- It is a useful framework for linking digital media to color printing technology and provides a color space for painters to better understand the challenges of mixing differently colored pigments.
- Many color evaluation tools refer to CIE LAB as “Lab”.
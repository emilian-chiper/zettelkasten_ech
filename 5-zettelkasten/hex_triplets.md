### Meta
2024-09-26 13:24
**Tags:** [[color_gamut_spaces_systems]] [[web_colors_hex_triplets]]
**Status:** #completed  

### Defining HEX Triplets
- A **HEX triplet** is a six-digit and 3-byte hexadecimal number used to represent a color in the hypertext markup language ([HTML]([[html]])), cascading style sheets([CSS]([[css]])), scalable vector graphics ([SVG]([[svg]])), extensible 3D graphics ([X3D]([[x3d]])), and other Web applications.
- The bytes refer to the RGB components of the color where:
	- byte 1 refers to the Red `#ff0000` value,
	- byte 2 refers to the Green `#00ff00` value,
	- byte 3 refers to the Blue `#0000ff` value.
- Hexadecimal notation uses 16 distinct symbols where:
	- `0-9` represent values `0` to `9` and
	- `A-F` represent values `10` to `15`.
- For a Web color, one byte represents a number in the range `00` to `FF`.
- If any of the three bytes has a color value that is less than 16 (in hexadecimal) or 10 (in decimal), it must be represented with a leading zero so that the triplet always has six digits.
- For example, pure yellow where `R = 255`, `G = 255`, and `B = 0` has a HEX triplet value of `#FFFF00`.
- It takes `24 bytes` to specify a given color in this notation system and the total number of colors that can be specified is `256**3` or `16,777,216`. 
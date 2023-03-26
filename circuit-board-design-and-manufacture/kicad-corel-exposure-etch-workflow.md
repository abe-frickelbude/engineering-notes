
# KiCad -> CorelDraw -> Exposure -> Etching Workflow

## KiCad data export

### PCB Artwork for @home board manufacture

* Use `Plot` and not `Print`
* Export only the `B.Cu` layer, and tick the `Plot Edge.Cuts on all layers` box to 
  include the board outline in the plot
* Set the `Drill marks` to `small`
* Do _not_ enable `mirrored` or `negative` plot (see below)
    * Negative plot may be useful for e.g. "double-exposing" a board after initial 
      etching to expose the pads only, to use the photoresist layer as solder mask
* Save as `SVG`

The exported configuration is correct `AS-IS` if printed directly and put with the 
`print-side` facing the photoresist layer.

## CorelDraw operations

### Import

* Simply import the SVG artwork exported from KiCad
* Keep in mind that depending on SVG object/curve structure, especially in artwork 
  containing text, CorelDraw sometimes has trouble when trying to group the
  artwork with additional geometry (e.g. putting an extra rectangle around artwork). In this
  case, it is advisable to do an `Ungroup all` on the artwork, and then group the
  resulting individual curves with the your own geometry.
* If you need to add any additional text or other asymmetrical graphics to the artwork, 
  keep in mind that they will need to be mirrored in order to "come out the in the right
  orientation" when exposed.

### Printing

* For the best overall control over exposure results it is advisable to use ~ 100g
  tracing paper instead of e.g. Mylar transparency sheets
* Print with maximum available DPI, disable any "fast" or "economode" options
* Do **NOT** mirror the print! The artwork, as exported by KiCad, is already in the
  correct orientation if it is put `print-side` facing the photoresist material during the
  exposure. This is also the recommended configuration as it minimizes light diffraction on
  the printed artwork and reduces "fuzziness" of the resulting exposed image.
* Use laser print density spray to evenly coat the print side before proceeding
  with exposure.
  * Note: when using tracing paper, this produces a significantly more pronounced
    increase in "blackness" and contrast than with a transparency sheet.

## UV Exposure

* Put the printed artwork with `print-side` facing the photoresist layer, and make
  sure the entire surface is straight and firmly held in place
* It is advisable to plan at least 1-2 mm of clearance around the artwork due to 
  board edges usually having some existing defects in the photoresist
  layer (e.g. the protective film tends to peel a little over time, especially
  on sheared boards, resulting in pre-exposure of the surfaces to ambient light)

### Making a test "gradient" 

* Do not follow the usual Internet-provided advice of "expose for x seconds, move
  one further, repeat etc. -> now you have the first pattern exposed for N * x seconds 
  blah blah". This is prone with errors and has the potential to produce very
  fuzzy edges in the exposed artwork due to repeated tiny amounts of shifting
  in the artwork.
* Instead, cut up the protective film into the desired number of sections using 
  a stable ruler and a sharp knife. When exposing, simply peel a single section,
  keep the film, expose for the actual desired number of seconds, then put the
  film back over the exposed section before repeating for the next one. This way,
  each section is always only exposed once.

### Notes on photoresist material

* The typical photoresist material as produced by e.g. `Bungard` DOES age, just
  like normal B/W photographic paper, and particularly old samples may yield
  wildly inconsistent and potentially nonsensical exposure results!
* Do not forget to remove any labels or tags from the `protective-film-side` of
  any newly purchased material - the adhesive on some labels has the tendency
  to "leech" through the film, given enough time. At some point this will
  damage the photoresist layer and produce ugly "shadows" in the exposed
  artwork.
* As an added protective measure, it is preferable store the board material 
  in a thick black envelope / box to minimize expose to ambient light.
* The protective film on the surface has a a nasty habit of deteriorating over
  time and develops a sticky black mess around the edges of a board. This gunk
  will stain your fingers/tools/artwork prints/etc and is difficult to remove 
  without aggressive solvents. Therefore, if/when using older board material, 
  be sure to cut off at least 5-10 mm of material around all board edges before
  trying to peel the protective film, then carefully inspect the new edges by
  peeling a tiny corner - further cut-offs may be necessary.

### Exposure time

* This will vary depending on the age of your board material, and the quality 
  as well as output power of your UV exposure device.
* The photoresist layer CAN be overexposed, so careful control over exposure
  time is essential.
  * When using e.g. a pro-sumer grade UV exposure box with ~ 32W output (4x 
    UV CCFL lamps, 8W per lamp) together with the aforementioned tracing 
    paper as medium, the minimum viable exposure time appears to be ~30 seconds.
  * The optimal exposure time tends towards 60-70 seconds

## Developing

* Use of sodium metasilicate is advisable as it is significantly less aggressive
  than e.g. NaOH and has a much lower probability of over-developing the photoresist.
* The developer concentration appears to be **crucial** to the process, higher 
  concentrations tend to strip the photoresist much more quickly and will destroy
  the artwork given little time.
  * Assuming the `SENO 4006` developer concentrate, the recommended proportion
    is 1:14 (i.e. 1 part developer, 14 parts cold water). In reality, this is 
    too aggressive, and the more benign and controllable proportion is ~ 1:20
  * With the above concentration, development time for a ~60 second exposure
    is approximately 60 seconds 
  * 

## Etching

* Use an aerated tank - aeration appears to be much more important for the
  etching process than the mere temperature of the etching solution (mostly
  because of mechanical agitation)
* Use sodium persulfate as etching reagent - don't bother with FeCL3 as it just
  makes a mess...
* Recommended proportion is `200 grams` of sodium persulfate per `1 liter` of water
* The optional solution temperature is ~ 50 C, but lower temperatures will
  work as well, but will result in longer etching times.
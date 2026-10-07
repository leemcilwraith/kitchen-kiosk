# kitchen-kiosk
Skylight / Cozyla clone with Home Assistant functionality. 

# Building the frame

![The finished frame](../images/frame-finished.jpg)

The frame turns a portable touchscreen into something that looks like a picture on the wall. It's made entirely from 6mm MDF, and it's built in two parts so the screen can come back out if you ever need to get at it:

- **The hood** - the face panel and four side strips, glued into one piece
- **The back** - a back panel and spacer frame that the monitor mounts to

The hood drops over the back and screws on through its top and bottom edges.

**Total cost:** about £14 of MDF, plus glue, filler and paint.

## Tools

- Jigsaw
- Drill with a pilot bit and a bit large enough for the jigsaw blade
- Straight edge and clamps
- Hand router with a 45° chamfer bit
- Sanding block and files
- Calipers, or a good steel rule

## Materials

- 6mm MDF sheet
- Wood glue
- Short fine screws (I used 3.5 x 20mm)
- VESA screws longer than the ones supplied with the mount (see Step 6)
- Wood filler
- Primer and paint
- Felt or foam tape

## Step 1 - Measure your monitor first

Don't trust the spec sheet. Measure the actual monitor with calipers, because there's almost no tolerance in this design.

Mine measured:

| | |
|---|---|
| Monitor body | 302 x 506 x 33mm |
| Bezel | 15mm left, top and bottom; **19mm right** |
| Visible display | 268 x 476mm |

The uneven bezel is the important part. The display sits 2mm off-centre on the monitor, so I sized everything around the **display** rather than the monitor body. That way the picture looks dead centre in the frame.

Check for buttons or ports on the edges of the monitor too. Anything on the sides will be covered by the frame.

## Step 2 - Work out your dimensions

These are my dimensions. If your monitor is different, use the formulas to adapt them.

![Construction diagram](../images/frame-diagram.jpg)

| Part | My size | Formula |
|---|---|---|
| Window | 270 x 478mm | Display + 2mm (1mm bezel reveal all round) |
| Face panel | 320 x 528mm | Window + 2 x border (I used 25mm) |
| Side strips - left and right (x2) | 528 x 45mm | Length = face height |
| Side strips - top and bottom (x2) | 308 x 45mm | Length = face width - 2 x 6mm |
| Strip depth | 45mm | Back panel + spacer + monitor depth (6 + 6 + 33) |
| Back panel | 306 x 514mm | Internal opening - 2mm |
| Spacer frame | 306 x 514mm | Same as back panel |

**Total depth:** 51mm (45mm strips + 6mm face).

**Symmetry check:** with the monitor positioned as in Step 6, the display sits 26mm from every outer edge of the frame, behind a 25mm border. That leaves a 1mm strip of bezel showing all round, so it looks even.

**A note on clearance:** at a 25mm border, there's only about 5mm around the monitor on three sides and 1mm on the right. It's tight but it works. If you want more breathing room, a 30mm border (330 x 538mm face) gives you about 10mm on three sides and 6mm on the right.

## Step 3 - Cut the face panel and window

![Cutting the window](../images/frame-window-cut.jpg)

Cut the window out of a single piece of MDF rather than making the face from four mitred strips. Mitre joints in 6mm MDF have almost no glue area, they're hard to get perfectly square, and they tend to crack or ghost through the paint over time as the MDF moves with heat and humidity.

1. Cut the face panel to size and mark the window 25mm in from every edge.
2. Drill a hole in each inside corner, just inside the line, so the jigsaw blade can get in.
3. Clamp a straight edge along each side as a fence, and cut a millimetre or so inside the line.
4. Sand or file back to the line, and square up the corners with a file.

The borders are flexible until the face is glued to the sides, so support the sheet well while you're cutting and don't lift it by one border.

## Step 4 - Chamfer the window

![The chamfered edge](../images/frame-chamfer.jpg)

Run a 45° chamfer around the inside edge of the window with a hand router. This is what gives it a proper picture-frame look, and it softens the step down to the screen.

Do a test pass on an offcut first to get the depth right.

## Step 5 - Build the hood

![Gluing the hood](../images/frame-hood-glue.jpg)

The side strips use butt joints, not mitres. The long sides run the full length, and the top and bottom pieces fit between them.

1. Cut the side strips: two at 528 x 45mm and two at 308 x 45mm.
2. Glue the four strips into a rectangle, with the short pieces between the long ones.
3. Glue the face panel on top, flush with the outside edges. The face covers the front of the joints, so the only visible join is a thin line on the top and bottom surfaces.
4. Clamp and check it's square before the glue sets, by measuring both diagonals.
5. Drill a few generous breathing holes in the top and bottom strips for airflow. The screen and the space behind it get warm.

## Step 6 - Build the back and mount the monitor

![The back panel and spacer](../images/frame-back.jpg)

1. Cut the back panel and spacer frame to 306 x 514mm. Make the spacer a perimeter frame that runs right to the edges of the back panel.
2. Glue the spacer to the back panel. This gives you a 12mm-thick edge to screw into through the hood.
3. Drill holes for the VESA mount and a cut-out for the cables.
4. Position the monitor 4mm from the top, bottom and left edges, and flush with the right edge (viewed from the front). This offset compensates for the uneven bezel.

VESA screws have to pass through the back panel and spacer, so the screws supplied with the mount won't be long enough. Get some about 12mm longer.

<!-- TODO: add a line on how the VESA area is packed out behind the monitor, if needed -->

**If your back panel comes out undersized:** mine came out at about 300mm wide instead of 306mm. Rather than gluing a strip onto the edge, cut the spacer frame accurately to the full 306 x 514mm and centre the back panel behind it. The spacer then gives the correct outer size and still provides the screw edge at the top and bottom. Measure the monitor position from the spacer's edges, not the back panel's.

## Step 7 - Finish and fit

![Painting](../images/frame-paint.jpg)

1. Fill the joins and any screw holes, then sand smooth.
2. Prime before painting. MDF edges soak up paint, so they may need an extra coat.
3. Paint the hood. <!-- TODO: add the paint and finish you used -->
4. Put felt or foam tape on the inside of the face where it meets the screen, so there's no pressure on the LCD.
5. Drop the hood over the back assembly.
6. Screw through the top and bottom of the hood into the spacer edge. Drill pilot holes first, because thin MDF edges split easily, and keep the screws well back from the corners.

<!-- TODO: add how the frame is fixed to or supported by the wall -->

![The finished panel in the kitchen](../images/frame-installed.jpg)

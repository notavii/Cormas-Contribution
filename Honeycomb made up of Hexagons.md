
# Create Honey-Comb like Structure made-up of Regular Hexagons in Cormas.
<div align="center">
  <img src="https://github.com/user-attachments/assets/587047a5-3452-42d0-9762-230253d85cac">
</div>
<br>

## Steps
  * Install Pharo,follow the installation guide: https://github.com/pharo-open-documentation/pharo-wiki/tree/master

  * Load cormas in Pharo, go through tutorial https://github.com/cormas/cormas/edit/master/README.md
 
  * Load Roassal Full Version -
  
    - Launch cormas image in your Pharo Launcher
  
    - Click on Library option in menu bar
  
    - Roassal >> Load >> Load Full Version

  <br>
  
  ## Run the Following code in Playground (Ctrl + O + P)

```st
  | canvas points size rows cols q r x y gridWidth gridHeight offsetX offsetY |
canvas := RSCanvas new. "Initialize the canvas"

"Define hexagon size and grid dimensions"
size := 20. "Radius of each hexagon (distance from center to corner)"
rows := 10. "Number of rows"
cols := 10. "Number of columns"

"Define hexagon shape (6 vertices with 30° rotation for pointy-top)"
points := Array new: 6.
1 to: 6 do: [ :i |
    | angle |
    angle := (i - 1) * 60 degreesToRadians.
    points at: i put: (size * ((angle + (30 degreesToRadians)) cos)) @ (size * ((angle + (30 degreesToRadians)) sin)).
].

"Calculate grid dimensions to determine center offset"
gridWidth := (cols * (size * (3 sqrt))) + (size * (3 sqrt) / 2).
gridHeight := rows * (size * 1.5).

"Calculate the offset to center the grid"
offsetX := gridWidth / -2. "Negative because we need to move left from center"
offsetY := gridHeight / -2. "Negative because we need to move up from center"

"Generate staggered hexagonal grid using odd-r offset coordinates"
0 to: rows - 1 do: [ :r | 
    0 to: cols - 1 do: [ :q | 
        | hex cellX cellY |
        
        "Create the hexagon"
        hex := RSPolygon new.
        hex points: points copy.
        hex color: Color green. "Fill color"
        hex borderColor: Color black; borderWidth: 2. "Border color and width"
        
        "Calculate base position with staggered offset"
        cellX := size * (3 sqrt) * q.
        cellY := size * (1.5 * r).
        
        "Apply staggered effect for odd rows"
        r odd ifTrue: [ cellX := cellX + (size * (3 sqrt) / 2) ].
        
        "Apply centering offset"
        cellX := cellX + offsetX.
        cellY := cellY + offsetY.
        
        hex position: cellX @ cellY.
        canvas add: hex.
    ].
].

"Display the canvas"
canvas open.

```
## Modifications

**You can change color, number of rows columns, radius of hexagons, and border width & its color.**

## To be added more....

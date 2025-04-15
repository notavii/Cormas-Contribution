
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


size := 20. "Radius of each hexagon (distance from center to corner)"
rows := 10. "Number of rows"
cols := 10. "Number of columns"


points := Array new: 6.
1 to: 6 do: [ :i |
    | angle |
    angle := (i - 1) * 60 degreesToRadians.
    points at: i put: (size * ((angle + (30 degreesToRadians)) cos)) @ (size * ((angle + (30 degreesToRadians)) sin)).
].


gridWidth := (cols * (size * (3 sqrt))) + (size * (3 sqrt) / 2).
gridHeight := rows * (size * 1.5).


offsetX := gridWidth / -2. "Negative because we need to move left from center"
offsetY := gridHeight / -2. "Negative because we need to move up from center"


0 to: rows - 1 do: [ :r | 
    0 to: cols - 1 do: [ :q | 
        | hex cellX cellY |
        
      
        hex := RSPolygon new.
        hex points: points copy.
        hex color: Color green. "Fill color"
        hex borderColor: Color black; borderWidth: 2. "Border color and width"
        
       
        cellX := size * (3 sqrt) * q.
        cellY := size * (1.5 * r).
        
        
        r odd ifTrue: [ cellX := cellX + (size * (3 sqrt) / 2) ].
        
       
        cellX := cellX + offsetX.
        cellY := cellY + offsetY.
        
        hex position: cellX @ cellY.
        canvas add: hex.
    ].
].


canvas open.

```

## Modifications
You can change **color**, number of **rows, columns, radius** of hexagons, and **border width** & its **color**. 

## To be added more....

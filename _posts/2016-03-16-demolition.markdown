---
title:  "Making Demolition Decision Using ArcGIS"
date:   2016-03-16 21:05:23
categories: GIS
tags: GIS, ArcGIS
---
I developed this model to simulate simple random motion and biased random motion within constrained space. The major difference with the [previous model](https://flyingsiying.github.io/2016/netlogo1/) is that this model loads pre-created GIS data to generate NetLogo data.

How this model works:
* This program loads the GIS data of the Ohio State University buildings and pavement from
shapefiles.
* It generates NetLogo data and picks a random building as a `target` for student movement.
* It generates up to 200 students at random buildings.
* It allows students to move only within buildings (green patches) and orange patches (pavement).
* User can define whether student motion is random or biased towards the target building. `random-motion` involves a simple heuristic - test whether the patch in front of the student is feasible (green or orange); if so, move forward to that patch. If not, a student makes a random left turn. With `biased-motion`, a student turns to face the target after a successful move forward.
* `test-arrival` tests if a student is within 5 units of the target. If so, the student moves to that target, is removed, and the arrival-count is incremented.

Demo:
![](/images/demo/osu.gif)


To set up, the model loads the GIS data and sets the envelope for the NetLogo world.
``` ruby
extensions [ gis ]
globals [ pavement building centroid arrival-count target]
breed [building-labels building-label]
breed [target-building-labels target-building-label] ; this breed is not necessarily used in my code
breed [students student]

to set-up
  ca
  set pavement gis:load-dataset "OSU_data/pavement.shp"
  set building gis:load-dataset "OSU_data/buildings.shp"
  gis:set-world-envelope (gis:envelope-union-of
    (gis:envelope-of pavement)
    (gis:envelope-of building) )
  set arrival-count 0  ; reset the number of arrived students
  reset-ticks
end
```

`hide-labels` and `show-labels` ask the building-labels to show themselves.
```ruby
to display-buildings
  ask building-labels [die]
  gis:set-drawing-color green
  gis:draw building 3
    foreach gis:feature-list-of building
    [ set centroid gis:location-of gis:centroid-of ?
      if not empty? centroid
      [ create-building-labels 1
          [ set xcor item 0 centroid
            set ycor item 1 centroid
            set size 0
            set label gis:property-value ? "BLDG_NAME" ] ] ]
end


to display-pavement
  gis:set-drawing-color red
  gis:draw pavement 1
end


to hide-labels
  ask building-labels [hide-turtle]
end


to show-labels
  ask building-labels [show-turtle]
end
```

`create-buildings` generates green patches based on the building shapefile. `create-paths` generates orange patches based on the pavement shapefile. A random building (building-label) is designated as the target.

```ruby
to create-NetLogo-data
  create-buildings
  create-paths
end


to create-buildings
  if not any? building-labels [display-buildings]
  ask building-labels [hide-turtle]
  ask patches gis:intersecting building
  [set pcolor green]
  set target one-of building-labels
  ask target [show-turtle]

end


to create-paths
  ask patches gis:intersecting pavement
  [ set pcolor orange ]
end
```

The model uses the input of `number-student` to create students at random green patches (buildings).
```ruby``
to generate-students
  ask n-of number-students patches with [pcolor = green]
  [ sprout-students 1 [
      set color white
      set shape "person student"
      set size 15 ]
  ]
end
```

`remove-students` asks students to die and resets the `arrvial-count`, the number of students who have arrived at the target.
```ruby
to remove-students
  ask students [die]
  set arrival-count 0
end
```

To initiate student movement, if `biased-motion` is switched on, students turn to face the target. Otherwise, they make a random left turn. Students can only move forward if the patch in front of them is feasible (either green or orange). If they move to the edge of the NetLogo world, they make a random left turn.
```ruby
to move-students
  if not any? students [ stop ]
  ask students [
     random-motion ; random motion of students
     test-arrival ; test if the student has arrived at the target
   ]
  tick
end


to random-motion
  ifelse patch-ahead 1 != nobody [  
    ifelse [pcolor] of patch-ahead 1 = green or [pcolor] of patch-ahead 1 = orange
    [ fd 1 ; the student moves forward to that patch
      if biased-motion [ face target]   ]   
    [ lt random-float 360 ]
    ]
  [ lt random-float 360 ]
end
```

`test-arrival` tests if a student is within five units of the target. Five patches is necessary since a building centroid may be in an interior courtyard and not part of the building. The optimal distance could be more or less. Arrived students will disappear from the NetLogo world.

```ruby
to test-arrival
  if (distance target) <= 5  [
    move-to target
    set arrival-count arrival-count + 1
    die ]
end
```

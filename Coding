turtles-own
[
   class
   opinion
   attitude
]
patches-own
[
   patches_class
   medias_opinion
]
to setup
   clear-all
   reset-ticks
   create-medias
   create-netizens
   create-hardcores
   create-leaders
end
to go

   ask patches with [patches_class = "Media"]
   [
     let targets turtles with [class = "Netizen" and distance myself <= 20 ]
     ask targets
     [
       if (medias_opinion > 0 and abs ( medias_opinion - opinion ) < 1 and abs opinion < 1 )
       [ set opinion opinion + 0.1]

       if (medias_opinion < 0 and abs ( opinion - medias_opinion ) < 1 and abs opinion < 1 )
       [ set opinion opinion - 0.1]
     ]
   ]
   ask turtles with [class = "Leader"]
   [   let temp_opinion opinion
     let targets turtles with [class = "Netizen" and distance myself <= 10]
     ask targets
     [
       if (temp_opinion > 0 and abs ( temp_opinion - opinion ) < 1 and abs opinion < 1)
       [ set opinion opinion + 0.1]

       if (temp_opinion < 0 and abs ( opinion - temp_opinion ) < 1 and abs opinion < 1)
       [ set opinion opinion - 0.1]
     ]
   ]

   ask turtles with [class = "Netizen"]
   [
    rt random 360
    fd 10
     let temp_opinion opinion
     let targets min-n-of 10 other turtles with [class = "Netizen"] [ distance myself ]
     let green_num 0
   ask targets with [attitude = "not-fear"]
     [
       if temp_opinion * opinion > 0
       [set green_num green_num + 1]

       if temp_opinion = 0 and opinion = 0
       [set green_num green_num + 1]
     ]

     let not_fear_num count targets with [attitude = "not-fear"]
     if not_fear_num > 0
     [
        ifelse green_num / not_fear_num >= Threshold
        [
          set attitude "not-fear"
          set color green
        ]
        [
          set attitude "fear"
 set color red    ]
     ]

     let R (sum [opinion] of targets) / 10
     set opinion   precision ( (temp_opinion + R ) / 2 ) 1
   ]

  ask turtles with [class = "Hardcore"]
   [
     rt random 360
     fd 10
  ]
   tick
   if ticks >= 100
   [stop]
end
to   show_label
   ifelse count turtles with [label = ""] != 0
   [
      ask turtles
      [
        set label opinion
        set label-color white
      ]
   ]
   [
      ask turtles
      [
        set label ""
        set label-color white
      ]
   ]
end

to create-medias
   ask n-of Media_num patches
     [
     set patches_class "Media"
     if Social_Intervention = "Strong"
     [
     set medias_opinion precision (random-float 0.9 + 0.1) 1
     ]

     if Social_Intervention = "Weak"
     [
       set medias_opinion precision (random-float 1) 1
     ]

     if Social_Intervention = "No"
     [
       set medias_opinion precision (random-float 2 - 1) 1
     ]
   ]

   ask patches with [patches_class = "Media" ]
   [
     if medias_opinion = 0
     [set pcolor gray]

     if medias_opinion > 0 and medias_opinion <= 1
     [set pcolor blue]

      if medias_opinion >= -1 and medias_opinion < 0
     [set pcolor orange]
   ]
end

to create-netizens
   create-turtles Netizen_num
   [
     set class "Netizen"
     set shape "person"
     set size 2
     setxy random-pxcor random-pycor
     set opinion precision (random-float 2 - 1) 1

     ifelse random 100 < 50
     [
       set attitude "fear"
       set color red
     ]

       [
       set attitude "not-fear"
       set color green
     ]

   ]
end

to create-hardcores
   create-turtles 10
   [
     set class "Hardcore"
     set shape "person"
     set size 2
     setxy random-pxcor random-pycor
     set opinion precision (random-float 2 - 1) 1
     set attitude "not-fear"
     set color green
   ]
end

to create-leaders
   create-turtles Leader_num
   [
     set class "Leader"
     set shape "person"
     set size 3
     setxy random-pxcor random-pycor
     set opinion precision (random-float 2 - 1) 1
     set attitude "not-fear"
     set color green
   ]
end

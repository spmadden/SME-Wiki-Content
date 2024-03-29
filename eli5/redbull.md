---
title: redbull
description: 
published: 1
date: 2023-09-20T23:10:21.916Z
tags: 
editor: markdown
dateCreated: 2023-09-11T01:28:17.552Z
---

Atmospheric Pressure $\rho = p_0 \cdot (1 - \frac{L \cdot h}{T_0} )^\frac{g \cdot M}{R \cdot L}$ where

-   $\rho$ = pressure at altitude
-   $p_0$ = standard pressure at sea level (101325 Pa)
-   $L$ = Temperature lapse rate (0.0065 K/m)
-   $h$ = The altitude in question
-   $T_0$ = standard temperature at sea level (288.15 K)
-   $g$= Earth surface gravitational acceleration (9.80665$m/s2$)
-   $M$ = Molar mass of dry air (0.0289644 kg/mol)
-   $R$ = Universal gas constant (8.31447 J/(mol•K))

Terminal Velocity $v = \sqrt{\frac{2\cdot m \cdot g}{\rho \cdot A \cdot C_d}}$ where

-   $v$ = velocity at the specified altitude
-   $m$ = Mass of falling object
-   $g$ = gravitational acceleration
-   $A$ = projected area of the object
-   $C_d$ = Coefficient of drag of the object
-   $\rho$ = Density of the fluid through which the object is falling

Density of Air $\rho = \frac{p}{R\_{specific} T}$ where

-   $p$ = Absolute pressure
-   $R\_{specific}$ = Specific gas constant for dry air (287.058 J/(kg·K))
-   $T$ = Absolute temperature

Gravity at Altitude $g = g_h = g_0 \cdot (\frac{R_e}{R_e + h})^2$ where

-   $g_h$ = Gravity at elevation
-   $g_0$ = Gravity at surface
-   $R_e$ = Mean radius of the Earth
-   $h$ = Elevation in question

Will need to combine these four functions over time and altitude (third order diff-eq?) to get the result.

Sources:

-   <http://en.wikipedia.org/wiki/Atmospheric_pressure>
-   <http://www2.avs.org/chapters/nccavs/pdf/AtmPres_at_Diff_Altitudes.pdf>
-   <http://en.wikipedia.org/wiki/Terminal_velocity>
-   <http://en.wikipedia.org/wiki/Density_of_air>


---
title: parabolic_reflection
description: 
published: 1
date: 2023-09-20T23:06:27.880Z
tags: 
editor: markdown
dateCreated: 2023-09-11T01:30:14.117Z
---

## Parabolic Reflection

The gain of a parabolic reflector can be defined using the equation

$G = \frac{\pi^2 * d^2}{\lambda^2}*e_a$

where

-   $G$ = the gain of the dish
-   $d$ = the diameter of the dish
-   $\lambda$ = the wavelength requested
-   $e_a$ = the efficiency of the aperture (.55 to .70) is common for dishes

with the beamwidth of the antenna being

$theta = \frac{k*\lambda}{d}$

where

-   $\theta$ = the half-power (3 dBi down) beamwidth
-   $k$ = a factor varying on the shape and reflective pattern of the dish (typical ~70 when $\theta$ is in degrees
-   $\lambda$ = the wavelength of the requested frequency
-   $d$ = diameter of dish

So with some basic math, the gain of the 6ft dish at GPS frequencies 1575.42 MHz,

-   $d$ = 1.829m
-   $\lambda$ = 0.19029m

$G = \frac{\pi^2 * 3.345241m^2}{0.0362102841m^2}*.55 = 501.4849$ times mag

$G = \frac{\pi^2 * 3.345241m^2}{0.0362102841m^2}*.70 = 638.2535$ times mag

To convert that into dB [isotropic](https://en.wikipedia.org/wiki/Isotropic_antenna), $dBi = 10*log(power)$

$G_{dbI} = 10 * log_{10}(501.4849) = 27.002$ dBi gain

$G_{dbI} = 10 * log_{10}(638.2535) = 28.049$ dBi gain

with a beamwidth of

$\theta = \frac{70 * 0.19029m}{1.829m} = 7.282°$

So with some basic math, the gain of the 6ft dish at GPS frequencies 10.455 GHz,

-   $d$ = 1.829m
-   $\lambda$ = 0.02855m

$G = \frac{\pi^2 * 3.345241m^2}{0.0008151025m^2}*.55 = 22278.0729$ times mag

$G = \frac{\pi^2 * 3.345241m^2}{0.0008151025m^2}*.70 = 28353.9109$ times mag

$G_{dbI} = 10 * log_{10}(22278.0729) = 42.478$ dBi gain

$G_{dbI} = 10 * log_{10}(28353.9109) = 44.526$ dBi gain

with a beamwidth of

$\theta = \frac{70 * 0.02855}{1.829m} = 1.0926°$

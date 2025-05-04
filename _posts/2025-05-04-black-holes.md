---
layout: post
title: "Black Holes In Haskell"
author: "Lukas N"
published: true
---
I find black holes extremely fascinating and have always wanted to dive a bit deeper into them.
In the spirit of progressing my programming and math skills while learning new things everyday,
I wrote this Haskell program to calculate the time it would take for you to reach the singularity
of a Schwarzschild Black Hole assuming you were falling radially. In the future I might expand
on this to calculate it for more complex black holes and situations. I did this not only to learn
a bit more about the basic maths behind gravity and black holes, but also to get into Haskell as
I've always wanted to dive a bit deeper into it.

```haskell
-- schwarzschild black hole is a non-rotating, uncharged black hole
-- event horizon is the boundary around a black hole marking the point of no return
--  for a schwarzschild black hole, this boundary is at the schwarzschild radius, r_s
--      r_s = (2GM/c^2)
-- the singularity is the center of a blackhole with infinite density
-- inside the singularity, proper time to the singularity is finite
--  will be calculating time as you experience it

-- tidal forces are the stretching and compressing due to gravity's variation across
--  your body
-- assume you are falling radially (straight in)

-- black hole at the center of the Milky Way is called Sagittarius A* (Sgr A*)
--  it has a mass 4.3 million times that of the sun
-- biggest blackhole that we know is Phoenix A
--  it has a mass 100 billion times that of the sun

-- units: meters, kilograms, seconds

--------------------------------------------------------------------------------

-- mass of our sun (kg)
sunM :: Double
sunM = 1.988e30

-- speed of light (m/s)
speedOfLight :: Double
speedOfLight = 2.99792458e8

-- gravitational constant (m^3 kg^-1 s^-2)
gravitationalConstant :: Double
gravitationalConstant = 6.6743e-11

-- n solar masses (>= 100,000) is a supermassive black hole
massBlackHole :: Int -> Double
massBlackHole n = sunM * fromIntegral n

-- (4GM)/3c^3
-- time from event horizon to the singularity (s)
properTimeToSingularity :: Double -> Double
properTimeToSingularity m = (4 * gravitationalConstant * m) / (3 * speedOfLight ^ 3)

formatTime :: Double -> String
formatTime seconds
    | seconds < 1e-3    = show (seconds * 1e6) ++ " microseconds"
    | seconds < 1.0     = show (seconds * 1e3) ++ " milliseconds"
    | seconds < 60.0    = show seconds ++ " seconds"
    | seconds < 3600.0  = show (seconds / 60.0) ++ " minutes"
    | otherwise         = show (seconds / 3600.0) ++ " hours"

main :: IO ()
main = do
    putStrLn $ "Mass of our sun: " ++ show sunM ++ " kg"
    let sgrAS = massBlackHole 4_300_000
    let m87 = massBlackHole 6_500_000_00
    let phoenixA = massBlackHole 100_000_000_000

    putStrLn $ "Mass of Sagittarius A* (at the center of the Milky Way): " ++ show sgrAS ++ " kg"
    putStrLn $ "Mass of M*& (the one we took a picture of): " ++ show m87 ++ " kg"
    putStrLn $ "Mass of Pheonix A (the biggest known black hole): " ++ show phoenixA ++ " kg"

    let sgrASTime = properTimeToSingularity sgrAS
    let m87Time = properTimeToSingularity m87
    let phoenixATime = properTimeToSingularity phoenixA

    putStrLn $ "Proper time to singularity for Sagittarius A*: " ++ formatTime sgrASTime
    putStrLn $ "Proper time to singularity for M*: " ++ formatTime m87Time
    putStrLn $ "Proper time to singularity for Phoenix A: " ++ formatTime phoenixATime
```

```
Mass of our sun: 1.988e30 kg
Mass of Sagittarius A* (at the center of the Milky Way): 8.5484e36 kg
Mass of M*& (the one we took a picture of): 1.2922e39 kg
Mass of Pheonix A (the biggest known black hole): 1.9880000000000002e41 kg
Proper time to singularity for Sagittarius A*: 28.23366043208198 seconds
Proper time to singularity for M*: 1.1855219173677833 hours
Proper time to singularity for Phoenix A: 182.3879872873513 hours
```

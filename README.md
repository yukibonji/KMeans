KMeans
============

This is a simple k-means clustering implemented in f# using the forgy method of initialization.  The clustering completes when the clusters datapoints converges (i.e. data points stop moving between clusters). You can also give an iteration limit on clustering if you want.

As an examle, the output for k=3 clustering for 100 float points in 1 dimesional space is. 

```
Generating data
.
Data generated
Centroid [17], with data points:
[0], [1], [2], [3], [4], [5], [6], [7], [8], [9], [10], [11], [12], [13], [14],
[15], [16], [17], [18], [19], [20], [21], [22], [23], [24], [25], [26], [27], [2
8], [29], ...

Centroid [51.5], with data points:
[35], [36], [37], [38], [39], [40], [41], [42], [43], [44], [45], [46], [47], [4
8], [49], [50], [51], [52], [53], [54], [55], [56], [57], [58], [59], [60], [61]
, [62], [63], [64], ...

Centroid [84], with data points:
[69], [70], [71], [72], [73], [74], [75], [76], [77], [78], [79], [80], [81], [8
2], [83], [84], [85], [86], [87], [88], [89], [90], [91], [92], [93], [94], [95]
, [96], [97], [98], ...

```


For multi-dimesional space, give each data point multiple elements. For example, a DataPoint with 2 points represents a 2D space.

Example output for k=3 clustering on a 2D space where each point is (x,x) where x goes from 0 to 100

```
Generating data
.
Data generated
Centroid [17; 17], with data points:
[0; 0], [1; 1], [2; 2], [3; 3], [4; 4], [5; 5], [6; 6], [7; 7], [8; 8], [9; 9],
[10; 10], [11; 11], [12; 12], [13; 13], [14; 14], [15; 15], [16; 16], [17; 17],
[18; 18], [19; 19], [20; 20], [21; 21], [22; 22], [23; 23], [24; 24], [25; 25],
[26; 26], [27; 27], [28; 28], [29; 29], ...

Centroid [51; 51], with data points:
[35; 35], [36; 36], [37; 37], [38; 38], [39; 39], [40; 40], [41; 41], [42; 42],
[43; 43], [44; 44], [45; 45], [46; 46], [47; 47], [48; 48], [49; 49], [50; 50],
[51; 51], [52; 52], [53; 53], [54; 54], [55; 55], [56; 56], [57; 57], [58; 58],
[59; 59], [60; 60], [61; 61], [62; 62], [63; 63], [64; 64], ...

Centroid [83.5; 83.5], with data points:
[68; 68], [69; 69], [70; 70], [71; 71], [72; 72], [73; 73], [74; 74], [75; 75],
[76; 76], [77; 77], [78; 78], [79; 79], [80; 80], [81; 81], [82; 82], [83; 83],
[84; 84], [85; 85], [86; 86], [87; 87], [88; 88], [89; 89], [90; 90], [91; 91],
[92; 92], [93; 93], [94; 94], [95; 95], [96; 96], [97; 97], ...
```


Example usage

```fsharp
open KMeans

let dimensions = 2
let dataPoints = 100
let kClusterValue = 3
let maxIterations = Int32.MaxValue
let convergenceDelta = 5.0 // if the distnace between subsequent cluster calculations is less than this then we can 
                           // just assume the clusters have converged enough. this is to keep clusters from never converging


let sampleData : KMeans.DataPoint list = KMeans.generateData dataPoints dimensions
                           
KMeans.clusterWithIterationLimit sampleData kClusterValue maxIterations convergenceDelta
    |> Seq.iter(KMeans.displayClusterInfo)

Console.ReadKey() |> ignore
```

Disclaimer
====

I'm not 100% sure the nDimesional centroid calculation is correct. I have it set up that it is the average of each dimesion, but I am not sure that is correct. If it's not right let me know!

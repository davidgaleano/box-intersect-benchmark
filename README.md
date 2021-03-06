# THE GREAT JAVASCRIPT BOX INTERSECTION BENCHMARK

The goal of this benchmark is to compare different solutions for finding all intersections amongst a set of boxes.  An overview of this problem and this procedure can be found in the following blog posts:

* [Collision detection (part 1)](http://0fps.net/2015/01/07/collision-detection-part-1/)
* [Collision detection (part 2)](http://0fps.net/2015/01/18/collision-detection-part-2/)
* [Collision detection (part 3)](http://0fps.net/2015/01/23/collision-detection-part-3-benchmarks/)

### Libraries surveyed

| Library | Algorithms implemented | Dimensions | Bipartite |
|:-------:|:----------------------:|:----------:|:---------:|
| None | Brute force | Any | ✓ |
| [box-intersect](https://github.com/mikolalysenko/box-intersect) | Streaming segment trees | Any | ✓ |
| [rbush](https://github.com/mourner/rbush) | BVH | 2 | ✓ |
| [p2.js](https://github.com/schteppe/p2.js) | Brute force, sweep and prune, grid | 2 | |
| [jsts](https://github.com/bjornharrtell/jsts) | BVH, hierarchical grid | 2 | ✓ |
| [rtree](https://github.com/leaflet-extras/RTree) | BVH | 2 | ✓ |
| [simple-quadtree](https://github.com/asaarinen/qtree) | Hierarchical grid | 2 | ✓ |
| [oimo](https://github.com/lo-th/Oimo.js/) | Brute force, BVH, sweep and prune | 3 | |
| [box2d](http://box2d.org/) | Sweep and prune | 2 | |
| [lazykdtree](https://github.com/0x0539/kdtree) | BVH | Any | ✓ |

# Results

Figures courtesy of [plot.ly](http://plot.ly)! Click on the images to get interactive plots

## 2D - Complete

### Uniform

<img src="https://mikolalysenko.github.io/box-intersect-benchmark/images/uniform.png">

#### Tiny (500 boxes)

[<img src="https://plot.ly/~MikolaLysenko/124/image.svg">](https://plot.ly/~MikolaLysenko/124)

#### Small (1500 boxes)

[<img src="https://plot.ly/~MikolaLysenko/125/image.svg">](https://plot.ly/~MikolaLysenko/125)

#### Medium (10000 boxes)

[<img src="https://plot.ly/~MikolaLysenko/127/image.svg">](https://plot.ly/~MikolaLysenko/127)

#### Large (250000 boxes)

[<img src="https://plot.ly/~MikolaLysenko/129/image.svg">](https://plot.ly/~MikolaLysenko/129)

### Circle

<img src="https://mikolalysenko.github.io/box-intersect-benchmark/images/sphere.png">

#### Small (10000 boxes)

[<img src="https://plot.ly/~MikolaLysenko/130/image.svg">](https://plot.ly/~MikolaLysenko/130)

#### Large (50000 boxes)

[<img src="https://plot.ly/~MikolaLysenko/131/image.svg">](https://plot.ly/~MikolaLysenko/131)

### High aspect ratio

<img src="https://mikolalysenko.github.io/box-intersect-benchmark/images/skewed.png">

#### Small (10000 boxes)

[<img src="https://plot.ly/~MikolaLysenko/132/image.svg">](https://plot.ly/~MikolaLysenko/132)

#### Large (100000 boxes)

[<img src="https://plot.ly/~MikolaLysenko/139/image.svg">](https://plot.ly/~MikolaLysenko/139)

## 2D - Bipartite

#### Small uniform (1500) vs Large uniform (50000)

[<img src="https://plot.ly/~MikolaLysenko/147/image.svg">](https://plot.ly/~MikolaLysenko/147)

#### Circle (20000) vs uniform (20000)

[<img src="https://plot.ly/~MikolaLysenko/148/image.svg">](https://plot.ly/~MikolaLysenko/148)

#### High aspect ratio (20000) vs uniform (20000)

[<img src="https://plot.ly/~MikolaLysenko/150/image.svg">](https://plot.ly/~MikolaLysenko/150)

#### Skewed (5000) vs circle (20000)

[<img src="https://plot.ly/~MikolaLysenko/151/image.svg">](https://plot.ly/~MikolaLysenko/151)

## 3D - Complete

#### Uniform

[<img src="https://plot.ly/~MikolaLysenko/152/image.svg">](https://plot.ly/~MikolaLysenko/152)

#### Sphere

[<img src="https://plot.ly/~MikolaLysenko/153/image.svg">](https://plot.ly/~MikolaLysenko/153)

#### Skewed

[<img src="https://plot.ly/~MikolaLysenko/154/image.svg">](https://plot.ly/~MikolaLysenko/154)

#### Bunny

[<img src="https://plot.ly/~MikolaLysenko/155/image.svg">](https://plot.ly/~MikolaLysenko/155)

# Running the benchmark

## In node.js/iojs

First, you will need to have [npm](https://www.npmjs.com/) installed and [git](http://git-scm.com/).  Clone this repo, go into the directory where it is located and then type:

```
npm install
```

To pull in all the files locally.  If you have node.js installed, you can then do,

```
node run
```

Or if you are using iojs,

```
iojs run
```

You can run specific cases by specifying them on the command line.  For example, to run the tiny benchmark do:

```
node run cases/uniform2d-tiny-complete.json
```

If you want to run the whole suite at once, you can run one of the following npm scripts:

```
npm run complete2
npm run bipartite2
npm run complete3
npm run bipartite3
```

These take some time to run so be patient!

### Setting up [plot.ly](https://plot.ly/)  (optional)

If you want to make charts to go along with your data, you will need to create an account and get an API key with [plot.ly](https://plot.ly/).  Once you've done this, save your credentials to the file `plotly.json` in the root directory of the folder (note this is not tracked in git).  The contents of the JSON file should look something like:

```javascript
{
  "username": "Node.js-Demo-Account",
  "key": "dvlqkmw0zm"
}
```

# Contributing

Improvements to these benchmarks are always welcome.  

## Adding more test data

To create a new generator, you can create a module in the `generators/` folder and add a reference to it in the distributions object in the `bench.js` file.  You can also create new test cases by modifying the JSON configuration files in the `cases/` folder.  The cases which are run

## Adding an algorithm

To add a new algorithm to the suite, there are 3 things you need to do:

1.  Create an adapter for the algorithm in the `algorithms/` folder.  At minimum, your adapter must implement two methods:  `exports.prepare` and `exports.run`.  
    a. `prepare` should translate the input boxes into whatever data format your algorithm requires (ie if you have some custom AABB type, then do these conversions here so you aren't penalized by them)
    a. `run` should execute your algorithm and return the total number of overlapping rectangles
2.  Add an entry in the `completeAlgs` or `bipartiteAlgs` sets in `bench.js`.  If your algorithm only supports one of these modes of entry (for example only complete intersections), then you don't have to add it to both tables.
3.  Add your algorithm to the relevant test cases.

You can run your test cases using the `run.js` command.

# License
(c) 2015 Mikola Lysenko. MIT License
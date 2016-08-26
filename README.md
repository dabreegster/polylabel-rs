# Polylabel-rs
A Rust implementation of the [Polylabel](https://github.com/mapbox/polylabel) algorithm
# How to Use
```rust
extern crate polylabel;
use polylabel::polylabel;

extern crate geo;
use geo::{Point, LineString, Polygon};

let coords = vec![
    (0.0, 0.0),
    (4.0, 0.0),
    (4.0, 1.0),
    (1.0, 1.0),
    (1.0, 4.0),
    (0.0, 4.0),
    (0.0, 0.0)
];
let ls = LineString(coords.iter().map(|e| Point::new(e.0, e.1)).collect());
let poly = Polygon(ls, vec![]);
let label_pos = polylabel(&poly, &0.10);
// Point(0.5625, 0.5625)
```
<img src="https://cdn.rawgit.com/urschrei/polylabel-rs/5ab07d193f61bb0e16338a6d19a08ba32f153ddb/ell.svg"/>

# FFI
Call `polylabel_ffi` with:
- `Array` (exterior Polygon ring)
- `WrapperArray` (interior Polygon rings)
- `tolerance` a `c_float`

The function returns a struct with two `c_double` fields:
- `x_pos`
- `y_pos`

A Python example is available in [`ffi.py`](ffi.py)
# License
[MIT](license.txt)

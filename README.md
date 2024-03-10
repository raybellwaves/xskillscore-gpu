# xskillscore-gpu

WIP: Run xskillscore on a GPU

## Background

### What is xskillscore?

A generic library to calculate skillscores but mostly for for weather/climate forecasts (xarray).

### How does xskillscore work?

xskillscore is mostly just a ufunc library that contains ufuncs that
are passed to [ `xarray.apply_ufunc`](https://docs.xarray.dev/en/stable/generated/xarray.apply_ufunc.html).

Functions are written in numpy 


# xskillscore-gpu

WIP: Run [xskillscore](https://github.com/xarray-contrib/xskillscore) on a GPU.

## How to implement


Ideally things work with zero code changes up the stack:
 - import numpy as np; gives you speed up for `numpy` operations if you have a GPU.
 - You can currently dispatch in `numpy` if you pass a cupy array (`np.absolute(cupy_array_forecasts, cupy_array_observations)`) to `numpy` functions which is a step towards zero-code changes.
 - xarray has 


## Why?

Goal of zero code changes if you are an xskillscore user and you have a GPU.

## Background

### What is xskillscore?

A generic library to calculate skillscores but mostly for for weather/climate forecasts (xarray).

### How does xskillscore work?

xskillscore is mostly just a ufunc library that contains ufuncs that
are passed to [ `xarray.apply_ufunc`](https://docs.xarray.dev/en/stable/generated/xarray.apply_ufunc.html).

Functions are written using `numpy` for `xarray.Dataset`'s and there
is acceleration built into xarray using `dask` and `numba`.

Traditional calcuation of skillscores happens using for loops. The example below is how someone could create the 
mean absolute error (MAE) for a few weather forecasts to create a 2D map (latitude, longitude) of MAE.
Here MAE is applied over the time dimension of two arrays (observations and forecasts).

```
mae = np.zeros((len(latitudes), len(latitudes))
for i lat in range(0, len(latitudes)):
    for j in range(0, len(latitudes)):
        mae[i, j] = np.absolute(forecasts[i, j, :], observations[i, j, :]
```

These for loops are essentially an embaraissingly parallel problem as they can be run independently.
This is what `xarray.apply_ufunc` does.




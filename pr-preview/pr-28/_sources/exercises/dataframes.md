# DataFrames Exercise

You can do this exercise in a notebook or as a script (or even in the REPL!).

## Load and Clean-up a DataFrame

Open the reduced Higgs ML dataset, that you will find in the `assets` area of this tutorial, if you cloned it or are running via Binder (or you can get it [here](https://github.com/JuliaHEP/JuliaHEP-2023/raw/main/julia-intro/docs/assets/atlas-higgs-challenge-2014-v2-reduced.csv)).

N.B. To understand the structure of the data, have a look at the [Higgs ML Website](https://higgsml.ijclab.in2p3.fr) and the [CERN Opendata Portal](https://opendata.cern.ch/record/328).

First, *clean* the dataset, replacing *all* of the numerical $-999.0$ values with the correct Julia `missing` values.

## Plot Primary Variables for Signal and Background

For the signal and background events (`Label == 's'`, `Label == 'b'` respectively), plot the tau and lepton $p_T$ and $(\eta, \phi)$.

This is a nice way to start to visualise if this is a significant variable for distinguishing signal from background.

If scatter plots are too busy, you could subsample the data using the usual Julia slice notation, `[start:step:end]`.

### Summary Values

Using the `Statistics` package, find the mean and standard deviation for the tau and lepton $p_T$ (try to use the original data frame and `groupby`).

## Derive Data and Plot

Calculate the distance metric between the tau and the lepton, 
$d = \sqrt{(\eta_\tau - \eta_{lep})^2 + (\phi_\tau - \phi_{lep})^2}$

Remember that $\delta\phi$ should be normalised.

## Next Steps

For this exercise we haven't really time to do much more than this initial data exploration.
If you wanted to take this further, a nice direction is to learn the basics of one of the
nice Julia ML packages (`MJL.jl` or `Flux.jl`) and start training some ML networks to distinguish
the Higgs events from the background. After all, that is exactly the *raison d'être* of this dataset!

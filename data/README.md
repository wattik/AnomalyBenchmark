# Datasets

## Anomaly datasets

There are several types of anomalies in data streams. We categorize them in the following way:
- neatData – clean data sets generated with no anomalies. Eg. sine, constant, spike train.
- corruptedData – these data sets were taken from the previous group but then corrupted by a deterministic anomaly. Subfolders comprise datasets grouped by the category. Such as: point anomaly, section anomaly, etc. See the subfolders article.
		
Each of these folders contain source data and results generated in a HTM experiment.

## Data sets structure

Data are stored in cvs files with columns: timestamp, function, phase, has_anomaly.
- `time` – time in seconds
- `function` – an output of the given function `f(t)`
- `phase` – a real number addressing in which phase the given periodic function is. For instance, `phase` column would include numbers from `0` to `2*pi`, following the phase of sinus. 
- `has_anomaly` – boolean, if `i`-th sample contains anomaly, 'anomaly at `i`-th row' = 1, otherwise 0.

Results are cvs files as well. They contain additional columns: anomaly_score, anomaly_likelihood.
- `anomaly_score` – raw anomaly score generated by HTM core
- `anomaly_likelihood` – likelihood generated by HTM core

## Why we use an 'ugly' `f = 1.001 Hz`?

We use data that are generated by a single frequency function, eg. 1 Hz sine or a spike train. The frequency of the function is `f`. Then, we sample the continuous function with the sampling frequency `fs`. Having considered the sampling theorem, we get a ratio `K = fs/f > 2`. If the ratio `K` is a natural number, what we get is a sequence of `K` numbers which are repeated exactly the same over and over again. 

The algorithm then does not create a model of the input data (sine function eg.), but it creates a model of a numbers series. That is a different task and, in fact, immensely easier. If we ensure an ugly real number, then there is a great chance we do not have any numbers series in the data. As a result, the algorithm really develops the model of the function with the given parameters.

## Subfolders

- datasets
  - corruptedData
    - point anomaly
      - amplitude
    - section anomaly
      - amplitude
      - dataLoss
      - noise
  - neatData
    - realworld
    - synthetic
- generatinScripts
	
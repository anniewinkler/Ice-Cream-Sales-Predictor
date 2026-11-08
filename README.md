# Ice Cream Sales Predictor (temperature & precipitation)

Pick a city and a date. The app asks a free weather API for the forecast high and the total
precipitation (rain + showers + snow), gives both to a trained model, and shows the predicted
number of cones sold, with a short business message.

- The model has two predictors: temperature and precipitation
- The app shows the forecast precipitation and warns when it is more than the model learned from.

## Files
- `app.py`: the Streamlit app
- `model.pkl`: the trained model (a linear regression with two predictors), saved from Colab
- `requirements.txt`: the packages Streamlit Cloud installs for you
- `Week3-Train-and-Save-Model.ipynb`: the Colab notebook that trains and saves `model.pkl`
- `Week3-Weather-API.ipynb`: the Colab notebook that explores the weather API

## How it works
1. The user picks a city and a date.
2. The app asks Open-Meteo (free, no key, no sign-up) for the forecast high (`temperature_2m_max`,
   in °F) and the precipitation total (`precipitation_sum`, in inches) for that day.
   `precipitation_sum` adds up rain, showers, and snowfall (snow as its water equivalent).
3. The model predicts sales from temperature and precipitation. The input table must have the
   columns `temperature` and `precipitation`, in that order, as in training.
4. The app shows the numbers, a warning if the temperature is outside 50 to 100 °F or the
   precipitation is above 2 inches per day (what the model learned from), and a short message.

The model was trained on made-up data, to show the steps. In that data, each extra degree adds
about 5 cones and each extra inch of precipitation removes about 60. Replace it with a model
trained on real data to use this for a real business.

## Cities
Pittsburgh, New York, Philadelphia, Chicago, Miami, Los Angeles, Rochester, Portland, Cleveland, and Seattle.

## Run it online for free (no terminal)
1. Put `app.py`, `model.pkl`, `requirements.txt` (and optionally `README.md`) in a public GitHub
   repository (upload them in the browser). The notebooks are optional.
2. On share.streamlit.io, create an app from the repository, main file `app.py`.
No API key is needed.

## If something goes wrong
- An error when loading `model.pkl`: check that the file is in the repository next to `app.py`,
  and that `scikit-learn` is listed in `requirements.txt`.
- An error such as "feature names should match": the model and the app are out of step. Make sure
  you uploaded the new `model.pkl` (two predictors), not the old one.
- An error about the forecast: the weather service may be busy. Wait a minute and try again.

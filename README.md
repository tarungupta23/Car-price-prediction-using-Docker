# Car Price Prediction — Resale Value Estimator

A complete, self-contained car price prediction website. 
## What it does

You enter three details about a used car:

| Column          | Meaning                                   |
|-----------------|--------------------------------------------|
| `Year`          | Manufacturing year                         |
| `Present_Price` | Original showroom price (in lakhs ₹)       |
| `Kms_Driven`    | Total kilometers driven                    |

...and it predicts `Selling_Price` — the estimated current resale value —
using a `RandomForestRegressor` trained with scikit-learn.

## Project structure

```
car-price-prediction/
├── train.py              # builds the dataset + trains + saves model.pkl
├── app.py                # Flask backend (serves the site + /predict API)
├── model.pkl             # trained model (already included, ready to use)
├── car_data.csv          # the dataset used for training
├── requirements.txt
├── templates/
│   └── index.html        # frontend page
└── static/
    ├── style.css          # dashboard / gauge styling
    └── app.js             # form handling + animated gauge
```

## How to run it on your machine

1. **Create a virtual environment (recommended)**

   ```bash
   python -m venv venv
   source venv/bin/activate      # on Windows: venv\Scripts\activate
   ```

2. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

3. **(Optional) Retrain the model**

   A trained `model.pkl` is already included, so you can skip this step.
   If you want to regenerate the dataset/model yourself:

   ```bash
   python train.py
   ```

   This creates `car_data.csv` and `model.pkl` in the project folder.

4. **Run the website**

   ```bash
   python app.py
   ```

5. **Open your browser** and go to:

   ```
   http://127.0.0.1:5000
   ```

   Fill in the year, showroom price, and kilometers driven, then click
   **Estimate Value** — the gauge on the right animates to show the
   predicted resale price, along with depreciation % and retained value %.

## Notes

- The dataset is generated synthetically inside `train.py` using a
  realistic depreciation formula (price falls with age and kms driven),
  so the whole project works completely offline.
- Swap in your own real-world dataset any time: just make sure it has
  columns named `Year`, `Present_Price`, `Kms_Driven`, `Selling_Price`
  and replace the `build_dataset()` step in `train.py` with
  `pd.read_csv("your_file.csv")`.
- This uses Flask's built-in development server, which is fine for
  local/demo use. For production, run it behind a WSGI server like
  gunicorn.

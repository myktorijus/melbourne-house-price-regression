<h1>Melbourne Housing Price Regression</h1>
<p>
  This repository contains a Jupyter Notebook project where I build and evaluate a linear regression model
  to predict house prices using the <strong>Melbourne Housing Market</strong> dataset from Kaggle.
  I use <strong>pandas</strong> for cleaning and EDA, <strong>matplotlib/seaborn</strong> for visualization,
  and <strong>statsmodels</strong> for ordinary least squares (OLS) regression.
  The goal is to estimate what a buyer should reasonably expect to pay given a property's characteristics,
  and to understand which features drive price the most.
</p>

<h2>Project Overview</h2>
<ul>
  <li><strong>Data source:</strong> Melbourne Housing Market dataset (Kaggle)</li>
  <li><strong>Key focus:</strong> data cleaning, EDA, leakage-safe preprocessing, and interpretable OLS regression</li>
  <li><strong>Outputs:</strong> an analysis notebook with charts, a fitted regression model, and interpreted results</li>
  <li><strong>Headline result:</strong> the model explains ~67% of price variation on unseen data (test R² = 0.674)</li>
</ul>

<h2>Repository Structure</h2>
<ul>
  <li><strong>data/</strong> — raw dataset (<code>Melbourne_housing_FULL.csv</code>)</li>
  <li><strong>notebook/</strong> — the main Jupyter Notebook (<code>analysis.ipynb</code>)</li>
  <li><strong>requirements.txt</strong> — project dependencies</li>
  <li><strong>README.md</strong> — project overview (how to run, what's inside, repo structure)</li>
</ul>

<h2>What's Inside the Notebook</h2>
<ul>
  <li><strong>Data loading & inspection</strong>: shape, dtypes, missing-value audit, summary statistics</li>
  <li><strong>Cleaning & validation</strong>:
    <ul>
      <li>dropping rows with missing target (<code>Price</code>)</li>
      <li>removing redundant / high-missingness columns with documented reasoning</li>
      <li>fixing erroneous values (e.g. <code>YearBuilt</code> = 1196)</li>
    </ul>
  </li>
  <li><strong>Exploratory Data Analysis</strong> (answered with visualizations):
    <ul>
      <li>Price distribution and the case for a log transformation</li>
      <li>Numeric variable distributions and skew</li>
      <li>Correlation heatmap against log(Price)</li>
      <li>Price variation by property type and region (boxplots)</li>
    </ul>
  </li>
  <li><strong>Leakage-safe preprocessing</strong>:
    <ul>
      <li>train/test split performed <em>before</em> any imputation</li>
      <li>median imputation and IQR outlier capping fit on the training set only</li>
      <li>one-hot encoding of categorical variables with a baseline reference</li>
      <li>empirical test of a log(Landsize) transform (tested and rejected — it increased skew)</li>
    </ul>
  </li>
  <li><strong>Modelling & evaluation</strong>:
    <ul>
      <li>OLS regression on log(Price) with numeric and categorical predictors</li>
      <li>metrics reported on the unseen test set: R², RMSE, and MAE in real AUD</li>
      <li>full interpretation of every coefficient (percentage effects via <code>exp(coef) − 1</code>)</li>
    </ul>
  </li>
  <li><strong>Key insights & suggested improvements</strong>: concise findings, limitations, and next steps</li>
</ul>

<h2>Key Findings</h2>
<ul>
  <li><strong>Property type</strong> is the strongest categorical driver — units are ~40% cheaper than houses.</li>
  <li><strong>Rooms</strong> is the strongest numeric driver — each additional room adds ~21% to price.</li>
  <li><strong>Location matters</strong> — region and distance from the CBD both significantly affect price.</li>
  <li>The model generalises well (train R² 0.682 vs test R² 0.674 — minimal gap, no overfitting).</li>
  <li>Typical prediction error (MAE) is ~$249k, roughly 29% of the median price — a useful ballpark, not a precise valuation.</li>
</ul>

<h2>How to Run</h2>
<ol>
  <li>Install Python 3.10+ (recommended)</li>
  <li>Create and activate a virtual environment</li>
  <li>Install dependencies:
    <pre><code>pip install -r requirements.txt</code></pre>
  </li>
  <li>Open and run the notebook:
    <ul>
      <li>in VS Code: open the <code>.ipynb</code> inside <code>notebook/</code> and select the project kernel</li>
      <li>or with Jupyter:
        <pre><code>jupyter notebook</code></pre>
      </li>
    </ul>
  </li>
</ol>

<h2>Notes</h2>
<ul>
  <li>All preprocessing (imputation, outlier capping, encoding) is fit on the training set only to prevent data leakage.</li>
  <li><code>BuildingArea</code> and <code>YearBuilt</code> were excluded due to excessive missingness (&gt;55%); recovering them via more advanced imputation (e.g. KNN) is noted as future work.</li>
  <li>This is a regression-focused project: the goal is an interpretable model and clear reasoning at each decision point, not maximum predictive accuracy.</li>
</ul>

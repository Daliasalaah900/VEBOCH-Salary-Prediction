Salary Prediction — Simple Linear Regression

Predicts an employee's salary from their years of experience using scikit-learn's LinearRegression, with exploratory plots and a Gradio demo UI.

Notebook: linear_regression.ipynb
Dataset: Salary_dataset.csv (not included — place it in the project folder)
Task: regression (target = Salary)
Dataset

30 rows, no missing values.

Column	Type	Description
Unnamed: 0	int	Row index leaked from a previous to_csv(). Not a real feature.
YearsExperience	float	Years of experience (1.2 – 10.6)
Salary	float	Target (37,732 – 122,392)
Workflow
Load the CSV and inspect it (head, tail, describe, info).
Explore with seaborn (jointplot, pairplot, lmplot).
Split the data: 70% train / 30% test, random_state=100.
Fit LinearRegression.
Evaluate with MAE, MSE, RMSE and a predicted-vs-actual scatter plot.
Serve predictions through a Gradio interface.
Results (as currently in the notebook)
Metric	Value
MAE	≈ 5,024
MSE	≈ 30,131,818
RMSE	≈ 5,489

Caveat: these numbers come from a model trained on YearsExperience and Unnamed: 0, and the test set is only 9 rows. Treat them as rough. Re-run after fixing the issues below.

Setup

pip

bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook linear_regression.ipynb

conda

bash
conda env create -f environment.yml
conda activate salary-prediction
jupyter notebook linear_regression.ipynb

The notebook reads /Salary_dataset.csv (a Colab-style absolute path). Change it to a relative path such as Salary_dataset.csv to run locally.

Known issues / TODO
Unnamed: 0 is used as a feature. It is just a row number. Drop it: pd.read_csv("Salary_dataset.csv", index_col=0), then use X = df[["YearsExperience"]].
The Gradio function takes Salary as an input. Salary is the target, so the model cannot take it as input. predict_spending should accept only YearsExperience (and be renamed, e.g. predict_salary).
Gradio input count is wrong. The interface declares 3 inputs (name, Salary, YearsExperience) but the function accepts 2, so Gradio warns and the app cannot work.
The last cell is copy-pasted from another project. It references Avg. Session Length, Time on App, etc., and crashes with KeyError. Delete it.
Tiny dataset. With 30 rows, consider cross-validation instead of a single split.
Project structure
salary-prediction/
├── linear_regression.ipynb
├── Salary_dataset.csv        # add this yourself
├── requirements.txt
├── environment.yml
└── README.md
Content
linear_regression.ipynb

IPYNB

Copy_of_Untitled1.ipynb

IPYNB

# Logistic-Regression

{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": 1,
   "id": "583ace36",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Logistic Regression model"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "id": "e9bca305",
   "metadata": {},
   "outputs": [],
   "source": [
    "#import libraries\n",
    "import pandas as pd"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "id": "a17ed111",
   "metadata": {},
   "outputs": [],
   "source": [
    "#Read the data and create a copy\n",
    "LoanData = pd.read_csv(\"01Exercise1.csv\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "id": "2aad0d8a",
   "metadata": {},
   "outputs": [],
   "source": [
    "LoanPrep = LoanData.copy()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "id": "e49d3f1d",
   "metadata": {},
   "outputs": [],
   "source": [
    "#identify the missing values"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "id": "307bdfb1",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "gender     13\n",
       "married     3\n",
       "ch         50\n",
       "income      0\n",
       "loanamt    22\n",
       "status      0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "LoanPrep.isnull().sum(axis=0)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "id": "55f455fb",
   "metadata": {},
   "outputs": [],
   "source": [
    "# droping the rows with missing values"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "id": "c05915cd",
   "metadata": {},
   "outputs": [],
   "source": [
    "LoanPrep = LoanPrep.dropna()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "id": "0488afa8",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>gender</th>\n",
       "      <th>married</th>\n",
       "      <th>ch</th>\n",
       "      <th>income</th>\n",
       "      <th>loanamt</th>\n",
       "      <th>status</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Male</td>\n",
       "      <td>Yes</td>\n",
       "      <td>1.0</td>\n",
       "      <td>4583</td>\n",
       "      <td>128.0</td>\n",
       "      <td>N</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Male</td>\n",
       "      <td>Yes</td>\n",
       "      <td>1.0</td>\n",
       "      <td>3000</td>\n",
       "      <td>66.0</td>\n",
       "      <td>Y</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Male</td>\n",
       "      <td>Yes</td>\n",
       "      <td>1.0</td>\n",
       "      <td>2583</td>\n",
       "      <td>120.0</td>\n",
       "      <td>Y</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Male</td>\n",
       "      <td>No</td>\n",
       "      <td>1.0</td>\n",
       "      <td>6000</td>\n",
       "      <td>141.0</td>\n",
       "      <td>Y</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>Male</td>\n",
       "      <td>Yes</td>\n",
       "      <td>1.0</td>\n",
       "      <td>5417</td>\n",
       "      <td>267.0</td>\n",
       "      <td>Y</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>609</th>\n",
       "      <td>Female</td>\n",
       "      <td>No</td>\n",
       "      <td>1.0</td>\n",
       "      <td>2900</td>\n",
       "      <td>71.0</td>\n",
       "      <td>Y</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>610</th>\n",
       "      <td>Male</td>\n",
       "      <td>Yes</td>\n",
       "      <td>1.0</td>\n",
       "      <td>4106</td>\n",
       "      <td>40.0</td>\n",
       "      <td>Y</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>611</th>\n",
       "      <td>Male</td>\n",
       "      <td>Yes</td>\n",
       "      <td>1.0</td>\n",
       "      <td>8072</td>\n",
       "      <td>253.0</td>\n",
       "      <td>Y</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>612</th>\n",
       "      <td>Male</td>\n",
       "      <td>Yes</td>\n",
       "      <td>1.0</td>\n",
       "      <td>7583</td>\n",
       "      <td>187.0</td>\n",
       "      <td>Y</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>613</th>\n",
       "      <td>Female</td>\n",
       "      <td>No</td>\n",
       "      <td>0.0</td>\n",
       "      <td>4583</td>\n",
       "      <td>133.0</td>\n",
       "      <td>N</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>529 rows × 6 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "     gender married   ch  income  loanamt status\n",
       "1      Male     Yes  1.0    4583    128.0      N\n",
       "2      Male     Yes  1.0    3000     66.0      Y\n",
       "3      Male     Yes  1.0    2583    120.0      Y\n",
       "4      Male      No  1.0    6000    141.0      Y\n",
       "5      Male     Yes  1.0    5417    267.0      Y\n",
       "..      ...     ...  ...     ...      ...    ...\n",
       "609  Female      No  1.0    2900     71.0      Y\n",
       "610    Male     Yes  1.0    4106     40.0      Y\n",
       "611    Male     Yes  1.0    8072    253.0      Y\n",
       "612    Male     Yes  1.0    7583    187.0      Y\n",
       "613  Female      No  0.0    4583    133.0      N\n",
       "\n",
       "[529 rows x 6 columns]"
      ]
     },
     "execution_count": 9,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "LoanPrep"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "id": "5b5486aa",
   "metadata": {},
   "outputs": [],
   "source": [
    "\n",
    "# Drop the irrelevant column of gender\n",
    "LoanPrep = LoanPrep.drop([\"gender\"],axis=1)\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "id": "4034bb06",
   "metadata": {},
   "outputs": [],
   "source": [
    "#Create dummy variable for categorical variables\n",
    "LoanPrep.dtypes\n",
    "\n",
    "LoanPrep = pd.get_dummies(LoanPrep, drop_first=True)\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "id": "f47dbf29",
   "metadata": {},
   "outputs": [],
   "source": [
    "#Normalize the data for loanamt and income using standard scaler\n",
    "\n",
    "from sklearn.preprocessing import StandardScaler\n",
    "scalar_ = StandardScaler()\n",
    "LoanPrep['income'] = scalar_.fit_transform(LoanPrep[['income']])\n",
    "LoanPrep['loanamt'] = scalar_.fit_transform(LoanPrep[['loanamt']])\n",
    "\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "id": "a79c054f",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>ch</th>\n",
       "      <th>income</th>\n",
       "      <th>loanamt</th>\n",
       "      <th>married_Yes</th>\n",
       "      <th>status_Y</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>1.0</td>\n",
       "      <td>-0.128073</td>\n",
       "      <td>-0.194250</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>1.0</td>\n",
       "      <td>-0.392077</td>\n",
       "      <td>-0.971015</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>1.0</td>\n",
       "      <td>-0.461621</td>\n",
       "      <td>-0.294478</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>1.0</td>\n",
       "      <td>0.108246</td>\n",
       "      <td>-0.031380</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>1.0</td>\n",
       "      <td>0.011017</td>\n",
       "      <td>1.547205</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>609</th>\n",
       "      <td>1.0</td>\n",
       "      <td>-0.408754</td>\n",
       "      <td>-0.908372</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>610</th>\n",
       "      <td>1.0</td>\n",
       "      <td>-0.207624</td>\n",
       "      <td>-1.296754</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>611</th>\n",
       "      <td>1.0</td>\n",
       "      <td>0.453802</td>\n",
       "      <td>1.371807</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>612</th>\n",
       "      <td>1.0</td>\n",
       "      <td>0.372249</td>\n",
       "      <td>0.544929</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>613</th>\n",
       "      <td>0.0</td>\n",
       "      <td>-0.128073</td>\n",
       "      <td>-0.131608</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>529 rows × 5 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "      ch    income   loanamt  married_Yes  status_Y\n",
       "1    1.0 -0.128073 -0.194250            1         0\n",
       "2    1.0 -0.392077 -0.971015            1         1\n",
       "3    1.0 -0.461621 -0.294478            1         1\n",
       "4    1.0  0.108246 -0.031380            0         1\n",
       "5    1.0  0.011017  1.547205            1         1\n",
       "..   ...       ...       ...          ...       ...\n",
       "609  1.0 -0.408754 -0.908372            0         1\n",
       "610  1.0 -0.207624 -1.296754            1         1\n",
       "611  1.0  0.453802  1.371807            1         1\n",
       "612  1.0  0.372249  0.544929            1         1\n",
       "613  0.0 -0.128073 -0.131608            0         0\n",
       "\n",
       "[529 rows x 5 columns]"
      ]
     },
     "execution_count": 13,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "LoanPrep"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "id": "9c685046",
   "metadata": {},
   "outputs": [],
   "source": [
    "#Build the logistic regression model"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "id": "213fe2e4",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Create the X (Independent) and Y (Dependent) dataframes"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "id": "9b31e473",
   "metadata": {},
   "outputs": [],
   "source": [
    "Y = LoanPrep[['status_Y']]\n",
    "X = LoanPrep.drop(['status_Y'], axis=1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "id": "fc4de4ec",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Split the X and Y dataset into training and testing set"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "id": "f63fc164",
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.model_selection import train_test_split\n",
    "\n",
    "X_train, X_test, Y_train, Y_test = train_test_split(X,Y,test_size=0.3, random_state=1234, stratify=Y)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "id": "5914c2a2",
   "metadata": {},
   "outputs": [],
   "source": [
    "#Build the logistic Regression model"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "id": "acff74cb",
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.linear_model import LogisticRegression"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "id": "73c925c9",
   "metadata": {},
   "outputs": [],
   "source": [
    "lr = LogisticRegression()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "id": "8f0d7735",
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "/usr/local/lib/python3.9/site-packages/sklearn/utils/validation.py:1111: DataConversionWarning: A column-vector y was passed when a 1d array was expected. Please change the shape of y to (n_samples, ), for example using ravel().\n",
      "  y = column_or_1d(y, warn=True)\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<style>#sk-container-id-1 {color: black;background-color: white;}#sk-container-id-1 pre{padding: 0;}#sk-container-id-1 div.sk-toggleable {background-color: white;}#sk-container-id-1 label.sk-toggleable__label {cursor: pointer;display: block;width: 100%;margin-bottom: 0;padding: 0.3em;box-sizing: border-box;text-align: center;}#sk-container-id-1 label.sk-toggleable__label-arrow:before {content: \"▸\";float: left;margin-right: 0.25em;color: #696969;}#sk-container-id-1 label.sk-toggleable__label-arrow:hover:before {color: black;}#sk-container-id-1 div.sk-estimator:hover label.sk-toggleable__label-arrow:before {color: black;}#sk-container-id-1 div.sk-toggleable__content {max-height: 0;max-width: 0;overflow: hidden;text-align: left;background-color: #f0f8ff;}#sk-container-id-1 div.sk-toggleable__content pre {margin: 0.2em;color: black;border-radius: 0.25em;background-color: #f0f8ff;}#sk-container-id-1 input.sk-toggleable__control:checked~div.sk-toggleable__content {max-height: 200px;max-width: 100%;overflow: auto;}#sk-container-id-1 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {content: \"▾\";}#sk-container-id-1 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 input.sk-hidden--visually {border: 0;clip: rect(1px 1px 1px 1px);clip: rect(1px, 1px, 1px, 1px);height: 1px;margin: -1px;overflow: hidden;padding: 0;position: absolute;width: 1px;}#sk-container-id-1 div.sk-estimator {font-family: monospace;background-color: #f0f8ff;border: 1px dotted black;border-radius: 0.25em;box-sizing: border-box;margin-bottom: 0.5em;}#sk-container-id-1 div.sk-estimator:hover {background-color: #d4ebff;}#sk-container-id-1 div.sk-parallel-item::after {content: \"\";width: 100%;border-bottom: 1px solid gray;flex-grow: 1;}#sk-container-id-1 div.sk-label:hover label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 div.sk-serial::before {content: \"\";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: 0;}#sk-container-id-1 div.sk-serial {display: flex;flex-direction: column;align-items: center;background-color: white;padding-right: 0.2em;padding-left: 0.2em;position: relative;}#sk-container-id-1 div.sk-item {position: relative;z-index: 1;}#sk-container-id-1 div.sk-parallel {display: flex;align-items: stretch;justify-content: center;background-color: white;position: relative;}#sk-container-id-1 div.sk-item::before, #sk-container-id-1 div.sk-parallel-item::before {content: \"\";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: -1;}#sk-container-id-1 div.sk-parallel-item {display: flex;flex-direction: column;z-index: 1;position: relative;background-color: white;}#sk-container-id-1 div.sk-parallel-item:first-child::after {align-self: flex-end;width: 50%;}#sk-container-id-1 div.sk-parallel-item:last-child::after {align-self: flex-start;width: 50%;}#sk-container-id-1 div.sk-parallel-item:only-child::after {width: 0;}#sk-container-id-1 div.sk-dashed-wrapped {border: 1px dashed gray;margin: 0 0.4em 0.5em 0.4em;box-sizing: border-box;padding-bottom: 0.4em;background-color: white;}#sk-container-id-1 div.sk-label label {font-family: monospace;font-weight: bold;display: inline-block;line-height: 1.2em;}#sk-container-id-1 div.sk-label-container {text-align: center;}#sk-container-id-1 div.sk-container {/* jupyter's `normalize.less` sets `[hidden] { display: none; }` but bootstrap.min.css set `[hidden] { display: none !important; }` so we also need the `!important` here to be able to override the default hidden behavior on the sphinx rendered scikit-learn.org. See: https://github.com/scikit-learn/scikit-learn/issues/21755 */display: inline-block !important;position: relative;}#sk-container-id-1 div.sk-text-repr-fallback {display: none;}</style><div id=\"sk-container-id-1\" class=\"sk-top-container\"><div class=\"sk-text-repr-fallback\"><pre>LogisticRegression()</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br />On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class=\"sk-container\" hidden><div class=\"sk-item\"><div class=\"sk-estimator sk-toggleable\"><input class=\"sk-toggleable__control sk-hidden--visually\" id=\"sk-estimator-id-1\" type=\"checkbox\" checked><label for=\"sk-estimator-id-1\" class=\"sk-toggleable__label sk-toggleable__label-arrow\">LogisticRegression</label><div class=\"sk-toggleable__content\"><pre>LogisticRegression()</pre></div></div></div></div></div>"
      ],
      "text/plain": [
       "LogisticRegression()"
      ]
     },
     "execution_count": 22,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "lr.fit(X_train,Y_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "id": "314bf8bf",
   "metadata": {},
   "outputs": [],
   "source": [
    "Y_predict =lr.predict(X_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 24,
   "id": "8f1edc42",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([0, 0, 1, 1, 1, 0, 1, 1, 0, 1, 1, 0, 1, 0, 0, 1, 1, 1, 1, 0, 1, 1,\n",
       "       1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 1, 1, 1, 0, 1, 1, 0, 1, 1, 1, 1, 1,\n",
       "       0, 0, 1, 1, 1, 1, 0, 1, 0, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,\n",
       "       1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1, 1, 1, 1, 0,\n",
       "       1, 1, 1, 0, 0, 1, 1, 1, 1, 1, 1, 1, 0, 1, 0, 1, 1, 1, 1, 1, 1, 1,\n",
       "       1, 1, 1, 0, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 0, 1, 1,\n",
       "       1, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1, 1, 0, 1, 1,\n",
       "       1, 1, 1, 1, 1], dtype=uint8)"
      ]
     },
     "execution_count": 24,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "Y_predict"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "id": "7be1b52e",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>status_Y</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>373</th>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>464</th>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>262</th>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>401</th>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>360</th>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>71</th>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>96</th>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>388</th>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>270</th>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>159 rows × 1 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "     status_Y\n",
       "373         0\n",
       "464         0\n",
       "3           1\n",
       "262         0\n",
       "401         0\n",
       "..        ...\n",
       "360         0\n",
       "71          1\n",
       "96          1\n",
       "388         1\n",
       "270         1\n",
       "\n",
       "[159 rows x 1 columns]"
      ]
     },
     "execution_count": 25,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "Y_test"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 26,
   "id": "e0342f81",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Build the confusion matrix and get the accuracy/score"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "id": "43abc302",
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.metrics import confusion_matrix, classification_report, accuracy_score"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 28,
   "id": "592892de",
   "metadata": {},
   "outputs": [],
   "source": [
    "cm = confusion_matrix(Y_test,Y_predict)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 29,
   "id": "a2e5256d",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([[ 29,  20],\n",
       "       [  2, 108]])"
      ]
     },
     "execution_count": 29,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "cm"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 30,
   "id": "4d750481",
   "metadata": {},
   "outputs": [],
   "source": [
    "score = lr.score(X_test,Y_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 31,
   "id": "4968e613",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.8616352201257862"
      ]
     },
     "execution_count": 31,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "score"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 32,
   "id": "70b0576d",
   "metadata": {},
   "outputs": [],
   "source": [
    "cr = classification_report(Y_test,Y_predict)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 33,
   "id": "b585ed55",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "              precision    recall  f1-score   support\n",
      "\n",
      "           0       0.94      0.59      0.72        49\n",
      "           1       0.84      0.98      0.91       110\n",
      "\n",
      "    accuracy                           0.86       159\n",
      "   macro avg       0.89      0.79      0.82       159\n",
      "weighted avg       0.87      0.86      0.85       159\n",
      "\n"
     ]
    }
   ],
   "source": [
    "print(cr)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 34,
   "id": "70001a9d",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.8616352201257862"
      ]
     },
     "execution_count": 34,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "score2 = accuracy_score(Y_test,Y_predict)\n",
    "score2"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 35,
   "id": "72f7896e",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Get the probabilities of the prediction"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 36,
   "id": "4dc68374",
   "metadata": {},
   "outputs": [],
   "source": [
    "Y_prob = lr.predict_proba(X_test)[:,1]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 37,
   "id": "9904d130",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([0.13205154, 0.13556507, 0.80585525, 0.72892604, 0.76368982,\n",
       "       0.17362279, 0.81174759, 0.78095461, 0.13348087, 0.75549986,\n",
       "       0.80985834, 0.08206817, 0.80891113, 0.16363003, 0.1684673 ,\n",
       "       0.8139622 , 0.7881667 , 0.73714535, 0.82284934, 0.13944529,\n",
       "       0.75852871, 0.73698161, 0.80998384, 0.73961229, 0.73662987,\n",
       "       0.74353726, 0.76951684, 0.7187181 , 0.80372215, 0.77871207,\n",
       "       0.11740852, 0.15979222, 0.81370741, 0.81304801, 0.78170526,\n",
       "       0.14353229, 0.83034976, 0.82288197, 0.1766822 , 0.82705651,\n",
       "       0.74526906, 0.744386  , 0.80515961, 0.82309065, 0.12545255,\n",
       "       0.09072906, 0.82153169, 0.74673919, 0.80562251, 0.83287524,\n",
       "       0.18188939, 0.81385427, 0.16591426, 0.78645433, 0.78731789,\n",
       "       0.18250139, 0.7091541 , 0.77210097, 0.79822718, 0.78404996,\n",
       "       0.74833446, 0.80229149, 0.74632792, 0.79058868, 0.7860087 ,\n",
       "       0.78837469, 0.83648173, 0.75872331, 0.7669137 , 0.77702998,\n",
       "       0.76390015, 0.69152131, 0.76568453, 0.80229078, 0.72744785,\n",
       "       0.80156838, 0.7353253 , 0.71202029, 0.80531283, 0.79427019,\n",
       "       0.17678202, 0.73252467, 0.80964214, 0.76878309, 0.82307494,\n",
       "       0.77006209, 0.81328862, 0.19247967, 0.81449667, 0.80835908,\n",
       "       0.80245701, 0.14130424, 0.17607466, 0.77875349, 0.77114641,\n",
       "       0.70836793, 0.81183803, 0.74314662, 0.80141119, 0.80726631,\n",
       "       0.18304613, 0.72042999, 0.17751525, 0.81276996, 0.75265373,\n",
       "       0.80526355, 0.76230011, 0.71734873, 0.82303971, 0.83185101,\n",
       "       0.81023084, 0.66935887, 0.81345511, 0.1505618 , 0.75096066,\n",
       "       0.80366594, 0.12666419, 0.73148664, 0.79003206, 0.8159927 ,\n",
       "       0.77446178, 0.78512469, 0.77401147, 0.8108012 , 0.82880229,\n",
       "       0.7885725 , 0.10748746, 0.73913258, 0.80640673, 0.15017735,\n",
       "       0.76689381, 0.78880269, 0.79980724, 0.15331563, 0.11416313,\n",
       "       0.80502898, 0.80198801, 0.74872806, 0.73093314, 0.7846734 ,\n",
       "       0.76152551, 0.75661939, 0.80285625, 0.73656308, 0.7471224 ,\n",
       "       0.80252088, 0.168792  , 0.80528478, 0.71576906, 0.78484134,\n",
       "       0.77900149, 0.13154009, 0.79021792, 0.80577789, 0.75878995,\n",
       "       0.8128528 , 0.80024731, 0.8005026 , 0.77676045])"
      ]
     },
     "execution_count": 37,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "Y_prob"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 38,
   "id": "52682b6a",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Create predictions based on probabilities\n",
    "Y_new_pred = []\n",
    "threshold = 0.785\n",
    "\n",
    "for i in range(0, len(Y_prob)):\n",
    "    if Y_prob[i] > threshold:\n",
    "        Y_new_pred.append(1)\n",
    "    else:\n",
    "        Y_new_pred.append(0)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 39,
   "id": "cbb5773d",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[0,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 1,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 0,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 1,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 1,\n",
       " 1,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 1,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 1,\n",
       " 1,\n",
       " 1,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 0,\n",
       " 0,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 1,\n",
       " 1,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 0,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 1,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 1,\n",
       " 1,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 1,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 1,\n",
       " 1,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 0,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 1,\n",
       " 0,\n",
       " 0,\n",
       " 0,\n",
       " 0,\n",
       " 1,\n",
       " 1,\n",
       " 0,\n",
       " 1,\n",
       " 1,\n",
       " 1,\n",
       " 0]"
      ]
     },
     "execution_count": 39,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "Y_new_pred"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 40,
   "id": "22bcf14f",
   "metadata": {},
   "outputs": [],
   "source": [
    "cm2 = confusion_matrix(Y_test,Y_new_pred)\n",
    "cr2 = classification_report(Y_test, Y_new_pred)\n",
    "score2 = accuracy_score(Y_test,Y_new_pred)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 41,
   "id": "e80060d7",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "[[44  5]\n",
      " [48 62]]\n"
     ]
    }
   ],
   "source": [
    "print(cm2)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 42,
   "id": "3d3601a6",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "              precision    recall  f1-score   support\n",
      "\n",
      "           0       0.48      0.90      0.62        49\n",
      "           1       0.93      0.56      0.70       110\n",
      "\n",
      "    accuracy                           0.67       159\n",
      "   macro avg       0.70      0.73      0.66       159\n",
      "weighted avg       0.79      0.67      0.68       159\n",
      "\n"
     ]
    }
   ],
   "source": [
    "print(cr2)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 43,
   "id": "fd94075e",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.6666666666666666"
      ]
     },
     "execution_count": 43,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "score2"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 44,
   "id": "17bd18e9",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Get the AUC and plot the Curve\n",
    "from sklearn.metrics import roc_curve,roc_auc_score\n",
    "fpr,tpr,threshold = roc_curve(Y_test,Y_prob)\n",
    "AUC = roc_auc_score(Y_test,Y_prob)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 50,
   "id": "fe84d0ca",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "import matplotlib.pyplot as plt\n",
    "plt.plot(fpr,tpr,linewidth=2)\n",
    "plt.xlabel(\"False Positive rate\")\n",
    "plt.ylabel(\"True Positive rate\")\n",
    "plt.title(\"ROC Curve for loan prediction\")\n",
    "plt.grid()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 46,
   "id": "c53bee09",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.8716141001855288"
      ]
     },
     "execution_count": 46,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "AUC"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "0997b1bc",
   "metadata": {},
   "outputs": [],
   "source": []
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3 (ipykernel)",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.9.9"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}

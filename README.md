# 🏈 Super Bowl LX Prediction Model

XGBoost Super Bowl prediction model. Found that defense and offense matter equally, but regular season wins? Completely irrelevant. Let's see if it's right.

---

Can machine learning predict the Super Bowl? I built an XGBoost binary classifier to analyze 25 years of Super Bowl data and find out what actually matters for winning.

**Prediction:** New England Patriots (56.7%) vs Seattle Seahawks (51.6%)  
**Model Edge:** Patriots favored, but it's close

---

## 📊 Key Findings

The most interesting part wasn't the prediction - it was what the data revealed:

- **Regular season wins literally don't matter** - Model gave it 0.0% importance. The 48% upset rate confirms this.
- **Defense and offense are equally important** - 36.6% vs 35.2%, nearly identical
- **Balanced teams win championships** - You need both sides of the ball

---

## 🛠️ Tech Stack

- **Model:** XGBoost (binary classification)
- **Hyperparameter Tuning:** GridSearchCV with 5-fold cross-validation
- **Data:** 50 rows (25 Super Bowls, 2000-2024 seasons)
- **Features:** Conference, Offensive Rank, Defensive Rank, Regular Season Wins
- **Tools:** Python, Pandas, Scikit-learn, Matplotlib, AWS S3, Google Colab

---

## 📁 Project Structure

```
├── Super60Prediction.ipynb         # Full analysis notebook
├── superbowl_historical_data.csv   # Training data (2000-2024)
└── README.md
```

---

## 🔍 Model Performance

- **Best CV Accuracy:** 67.5%
- **5-Fold Cross-Validation Mean:** 60.0%
- **Standard Deviation:** 0.063
- **ROC-AUC:** 0.48
- **Test Accuracy:** 40%

The low test accuracy reflects the reality: with only 50 data points and evenly matched teams, this genuinely is hard to predict. The model's honest answer is "these teams are close" - which is actually more valuable than false confidence.

---

## ⚠️ Model Limitation: Independent vs Head-to-Head Predictions

### What the Model Actually Does
The current model predicts each team **independently**:
- Seahawks: "What's your chance of winning a Super Bowl?" → 51.6%
- Patriots: "What's your chance of winning a Super Bowl?" → 56.7%

These probabilities don't add to 100% because they're separate predictions, not a direct comparison.

### Why This Happens
The training data has 50 rows (2 teams per game), where each row is labeled:
- 1 = this team won their Super Bowl
- 0 = this team lost their Super Bowl

The model learns "what makes a Super Bowl winner" but doesn't directly compare two teams against each other.

### The Better Approach (Head-to-Head)
A true head-to-head model would:
1. Restructure data to 25 rows (1 per game)
2. Use **differential features**: 
   - `off_rank_diff` = Team A offense - Team B offense
   - `def_rank_diff` = Team A defense - Team B defense
   - `wins_diff` = Team A wins - Team B wins
3. Predict: "Does the team with these advantages win?"

This would output proper relative probabilities (e.g., 55% vs 45%).

### Why I Kept It This Way
- Simpler to understand and explain
- Shows feature importance clearly (defense + offense matter, wins don't!)
- Still provides directional insight (Patriots have higher win probability)
- Honest about limitations

For a production model, I'd restructure for head-to-head comparison. For a learning project, this approach better demonstrates the fundamentals of binary classification and feature analysis.

---

## 🎯 Feature Importance

What matters most for winning the Super Bowl?

1. **Defensive Ranking** - 36.6%
2. **Offensive Ranking** - 35.2%
3. **Conference (NFC/AFC)** - 28.2%
4. **Regular Season Wins** - 0.0%

**Key insight:** Regular season wins literally don't matter at all to the model! Defense and offense are nearly equal (~36% and ~35%), confirming that balanced teams win championships. The 48% upset rate we found makes perfect sense now.

---

## 🚀 How to Run

```bash
# Clone the repo
git clone https://github.com/dingjamma/SuperbowlLXPrediction.git

# Open in Google Colab or Jupyter
# Make sure to install dependencies:
pip install pandas numpy xgboost scikit-learn matplotlib seaborn s3fs boto3

# Run the notebook cell by cell
```

Data is loaded from AWS S3. You'll need to set up your own AWS credentials if running locally.

---

## 💭 Reflections

This project taught me:
- Small datasets require careful interpretation
- Sometimes "I don't know" is the most honest answer
- Feature importance can reveal insights even when accuracy is low
- Regular season wins are meaningless for predicting Super Bowl winners
- Defense and offense matter equally - balance wins championships
- Model limitations are worth acknowledging

---

## 🎰 Beyond the Data: A Patriots Fan's Case

As a Brady diehard, my model gave Patriots a 56.7% edge - and here's why I think the betting market is undervaluing them:

### The Value Bet
- **My model:** Patriots 56.7% win probability
- **Betting market odds:** 2.95 (~33.9% implied probability)
- **The edge:** Model says Patriots are ~23% more likely to win than the market thinks

When your data shows value like that, you take the bet.

### Legacy & Pressure
- **Patriots only count rings.** They've never lost a Super Bowl except to underdog Giants (twice) and underdog Eagles. Something cursed about the NFC East.
- **Sam Darnold is emotionally weaker than Drake Maye.** Darnold's been the underdog his whole career - only QB from his draft class to make the Super Bowl (RIP Lamar, RIP Josh Allen). That pressure might crush him.
- **Drake Maye is fearless.** The chosen one. Tom Brady clone. 2nd year. Legendary organization. Main character energy. Thick plot armor.

### The Defense Isn't What It Seems
- **Rams exposed Seattle's #1 defense.** That ranking might be inflated. Maye can exploit it.

### The Bet
**239.08 CAD → 705.29 CAD if Patriots win** (odds: 2.95)

Data + gut feeling + market inefficiency. Let's ride. 🏈

Yeah, 500% cope but Patriots!

---

## 📝 Medium Article

https://medium.com/@dingjamma/nothing-else-matters-building-a-data-driven-super-bowl-prediction-model-6e647b79ad3c

---

## 📫 Connect

- LinkedIn: [jam-ding](https://www.linkedin.com/in/jam-ding)
- Medium: [@dingjamma](https://medium.com/@dingjamma)
- Email: james@dingjames.com

---

**Update after Super Bowl LX:** [TBD - Check back February 9, 2026]

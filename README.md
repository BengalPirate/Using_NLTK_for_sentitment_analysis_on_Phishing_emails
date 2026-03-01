# Phishing Email Sentiment Analysis with NLTK

A comprehensive Jupyter notebook project analyzing sentiment and language patterns in phishing versus legitimate emails using Python and NLTK's VADER sentiment analyzer.

## Table of Contents

- [Project Overview](#project-overview)
- [Quick Start](#quick-start)
- [Dataset](#dataset)
- [Requirements](#requirements)
- [Project Structure](#project-structure)
- [Methodology](#methodology)
- [Analysis Results](#analysis-results)
- [Notebook Contents](#notebook-contents)
- [Key Findings](#key-findings)
- [Troubleshooting](#troubleshooting)
- [References](#references)

## Project Overview

This project demonstrates natural language processing (NLP) and sentiment analysis techniques to understand how attackers use urgency, fear, and pressure in phishing emails. The analysis reveals significant differences in language patterns and emotional tone between phishing and legitimate communications.

**Assignment Objectives:**

- Load and explore a phishing email dataset
- Preprocess email text using NLTK tokenization and cleaning
- Perform sentiment analysis using VADER (Valence Aware Dictionary and sEntiment Reasoner)
- Compare sentiment scores between phishing and safe emails
- Identify common words and language patterns used in attacks

## Quick Start

### Step 1: Install Dependencies

```bash
pip install pandas nltk matplotlib seaborn jupyter
```

### Step 2: Launch Jupyter Notebook

```bash
jupyter notebook phishing_email_analysis.ipynb
```

### Step 3: Run All Cells

1. Click **Cell → Run All** in the menu
2. Wait for execution to complete (~30 seconds)
3. View results and visualizations inline

## Dataset

**Location:** `sample_email_dataset.csv`

**Statistics:**

- **Total emails:** 40
- **Phishing emails (label: phishing):** 20 (50.00%)
- **Safe emails (label: safe):** 20 (50.00%)
- **Features:** Email text content (text column)
- **File size:** ~3 KB

**Class Balance:** The dataset is perfectly balanced with equal representation of both classes, eliminating bias in analysis.

## Requirements

**Python Version:** 3.8+

**Required Packages:**

| Package | Purpose |
|---------|---------|
| `pandas` | Data manipulation and analysis |
| `nltk` | Natural language processing toolkit |
| `matplotlib` | Data visualization |
| `seaborn` | Statistical data visualization |
| `jupyter` | Interactive notebook environment |

**Installation:**

```bash
pip install pandas nltk matplotlib seaborn jupyter
```

**NLTK Data Downloads (automatic in notebook):**

- `punkt` - Tokenization models
- `stopwords` - Common English stopwords
- `vader_lexicon` - VADER sentiment analysis lexicon
- `punkt_tab` - Updated tokenization data

## Project Structure

```
AI_Detection_4/
├── sample_email_dataset.csv           # Main dataset (40 emails)
├── phishing_email_analysis.ipynb      # Main Jupyter notebook
└── README.md                          # This file
```

## Methodology

### 1. Text Preprocessing

Email text undergoes comprehensive cleaning using NLTK:

**Steps:**
1. **Tokenization** - Split text into individual words using `word_tokenize()`
2. **Lowercasing** - Convert all text to lowercase for consistency
3. **Stopword Removal** - Remove common English words (the, is, a, to, etc.)
4. **Punctuation Removal** - Strip special characters and punctuation

**Example:**

```
Original: "URGENT! Verify your account NOW at www.fake.com"
Tokens: ['URGENT', '!', 'Verify', 'your', 'account', 'NOW', 'at', 'www.fake.com']
Lowercased: ['urgent', '!', 'verify', 'your', 'account', 'now', 'at', 'www.fake.com']
Cleaned: ['urgent', 'verify', 'account', 'www.fake.com']
```

**Why This Matters:**
- Focuses analysis on meaningful content words
- Normalizes text for consistent comparison
- Reveals key terms attackers use for manipulation

### 2. Sentiment Analysis (VADER)

**VADER (Valence Aware Dictionary and sEntiment Reasoner):**

- Lexicon and rule-based sentiment analysis tool
- Specifically designed for social media and short texts
- Considers punctuation (!!!), capitalization (URGENT), and emoticons
- Returns four sentiment scores:
  - `neg` - Negative sentiment (0 to 1)
  - `neu` - Neutral sentiment (0 to 1)
  - `pos` - Positive sentiment (0 to 1)
  - `compound` - Overall sentiment score (-1 to +1)

**Compound Score Interpretation:**
- **+1.0** = Most positive sentiment
- **0.0** = Neutral sentiment
- **-1.0** = Most negative sentiment

**Analysis Focus:** We use the `compound` score as the primary metric for comparing phishing vs. safe emails.

### 3. Feature Extraction

**Word Frequency Analysis:**
- Extract most common words from cleaned tokens
- Compare vocabulary differences between phishing and safe emails
- Identify attacker tactics and language patterns

## Analysis Results

### Sentiment Score Summary

| Metric | Phishing Emails | Safe Emails | Difference |
|--------|-----------------|-------------|------------|
| **Average Sentiment** | **0.1042** | **0.1678** | **0.0636** |
| Minimum Score | -0.5719 | 0.0000 | - |
| Maximum Score | 0.7840 | 0.6908 | - |
| Standard Deviation | 0.3591 | 0.2481 | - |

**Key Observation:** Phishing emails have a **lower average sentiment score** (0.1042) compared to safe emails (0.1678), reflecting more negative and threatening language.

### Sentiment Distribution Analysis

**Phishing Emails:**
- **Mean:** 0.1042 (slightly positive overall, but with significant variation)
- **Range:** -0.5719 to 0.7840 (wide range indicating diverse tactics)
- **Std Dev:** 0.3591 (high variability in sentiment approaches)

**Safe Emails:**
- **Mean:** 0.1678 (moderately positive)
- **Range:** 0.0000 to 0.6908 (more consistent, professional tone)
- **Std Dev:** 0.2481 (lower variability, more predictable communication)

### Extreme Examples

**Most Negative Email:**
- **Label:** Phishing
- **Score:** -0.5719
- **Text:** "Confirm your password to avoid service interruption."
- **Analysis:** Uses threat ("avoid interruption") and urgency to create fear

**Most Positive Email:**
- **Label:** Phishing
- **Score:** 0.7840
- **Text:** "Congratulations! You have been selected for a special offer."
- **Analysis:** Uses excitement and exclusivity to lure victims (reward-based phishing)

### Top 10 Most Common Words

#### Phishing Emails

| Rank | Word | Frequency | Pattern Type |
|------|------|-----------|--------------|
| 1 | account | 5 | Target object |
| 2 | confirm | 4 | Action demand |
| 3 | verify | 3 | Action demand |
| 4 | detected | 3 | Urgency trigger |
| 5 | review | 3 | Action demand |
| 6 | information | 2 | Data request |
| 7 | immediately | 2 | Urgency word |
| 8 | click | 2 | Action demand |
| 9 | could | 2 | Conditional threat |
| 10 | update | 2 | Action demand |

**Phishing Language Patterns:**
- Action verbs: confirm, verify, review, click, update
- Urgency indicators: immediately, detected
- Target: account, information
- Conditional language: could (implying consequences)

#### Safe Emails

| Rank | Word | Frequency | Pattern Type |
|------|------|-----------|--------------|
| 1 | attached | 3 | Information sharing |
| 2 | scheduled | 3 | Planning |
| 3 | thank | 3 | Courtesy |
| 4 | team | 2 | Collaborative |
| 5 | meeting | 2 | Professional context |
| 6 | next | 2 | Future planning |
| 7 | reminder | 2 | Helpful notice |
| 8 | project | 2 | Work context |
| 9 | successfully | 2 | Confirmation |
| 10 | updated | 2 | Status indicator |

**Safe Email Language Patterns:**
- Informative: attached, scheduled, reminder, updated
- Collaborative: team, meeting, project
- Polite: thank
- Neutral tone: successfully, next

## Notebook Contents

The Jupyter notebook is organized into 11 comprehensive sections:

### Section 1: Setup
- Import required libraries
- Download NLTK data packages
- Configure visualization settings

### Section 2: Part 1 - Load & Inspect Data
- Load CSV file using pandas
- Display first 5 rows
- Count phishing vs safe emails
- Visualize distribution with bar chart
- Print 3 example phishing emails
- Print 3 example safe emails
- **Deliverable:** Code + explanation

### Section 3: Part 2 - Preprocessing with NLTK
- Define preprocessing function
- Apply tokenization, lowercasing, stopword removal, punctuation removal
- Show original vs cleaned text examples for phishing emails
- Show original vs cleaned text examples for safe emails
- **Deliverable:** Code showing original email and cleaned token list

### Section 4: Part 3 - Sentiment Analysis
- Initialize VADER sentiment analyzer
- Compute sentiment scores for all emails
- Add `sentiment_score` column to dataframe
- Calculate average sentiment for phishing emails: **0.1042**
- Calculate average sentiment for safe emails: **0.1678**
- **Deliverable:** Sentiment score calculations and comparison

### Section 5: Visualizations
- Bar chart comparing average sentiment scores
- Histogram showing sentiment distribution
- Detailed sentiment statistics

### Section 6: Extreme Examples Analysis
- Most negative email (phishing, -0.5719)
- Most positive email (phishing, 0.7840)

### Section 7: Bonus - Common Words Analysis
- Top 15 words in phishing emails
- Top 15 words in safe emails
- Visual comparison with text-based bar charts

### Section 8: Summary & Conclusions
- Key takeaways from analysis
- Language pattern observations
- Security implications
- NLTK tools used

## Key Findings

### Strengths

**1. Sentiment Differentiation**
- Phishing emails show **lower average sentiment** (0.1042 vs 0.1678)
- Greater variability in phishing (std: 0.3591) reflects diverse attack tactics
- Safe emails maintain consistent, professional tone (std: 0.2481)

**2. Language Pattern Detection**
- **Phishing vocabulary:** Heavy use of action verbs (verify, confirm, click)
- **Urgency indicators:** immediately, detected, account
- **Safe vocabulary:** Informative and collaborative (attached, scheduled, thank, team)

**3. Dual Phishing Tactics Identified**
- **Fear-based:** Negative sentiment (-0.5719) using threats and warnings
- **Reward-based:** Positive sentiment (0.7840) using congratulations and offers

**4. VADER Effectiveness**
- Successfully captures emotional tone differences
- Identifies threatening language in phishing attempts
- Detects fake positive language in reward-based phishing

### Limitations

**1. Small Dataset**
- Only 40 emails (20 phishing, 20 safe)
- Limited generalizability to real-world email volumes
- May not represent all phishing tactics

**2. Text-Only Analysis**
- Does not consider:
  - Email headers and metadata
  - Sender reputation
  - URL/link analysis
  - Attachment characteristics
  - HTML formatting and images

**3. Sentiment Ambiguity**
- Some phishing emails use positive sentiment (congratulations, rewards)
- Sentiment alone insufficient for detection
- Requires combination with other features

**4. Language Evolution**
- Phishing tactics constantly evolve
- Dataset reflects current tactics only
- Requires continuous updating

**5. Cultural and Linguistic Bias**
- VADER optimized for English text
- May not work well for non-English emails
- Cultural differences in communication styles

### Insights and Observations

**Attack Psychology:**
1. **Fear Tactics:** Threatening consequences (account suspension, service interruption)
2. **Urgency Creation:** Time pressure (immediately, now, final notice)
3. **Authority Impersonation:** Formal language mimicking legitimate services
4. **Reward Manipulation:** Fake offers to create excitement and lower guard

**Defensive Indicators:**
Users should be suspicious of emails containing:
- Multiple urgency words
- Demands for immediate action
- Requests to verify/confirm account information
- Threats of negative consequences
- Unexpected rewards or special offers

### Future Improvements

**Analysis Enhancements:**
1. **Larger Dataset:** Analyze thousands of emails for statistical significance
2. **Multi-Feature Analysis:** Combine sentiment with URL reputation, sender verification, header analysis
3. **Topic Modeling:** Use LDA or NMF to identify common phishing themes
4. **Named Entity Recognition:** Detect impersonated brands and organizations
5. **Temporal Analysis:** Study how phishing tactics evolve over time

**Advanced NLP Techniques:**
1. **Word Embeddings:** Use Word2Vec or GloVe for semantic analysis
2. **Deep Learning:** LSTM or BERT models for context understanding
3. **Urgency Detection:** Custom classifier for urgency language
4. **Readability Metrics:** Analyze text complexity and professionalism

**Real-World Application:**
1. **Machine Learning Classifier:** Train supervised model using sentiment + other features
2. **Real-Time Detection:** API integration for live email scanning
3. **User Feedback Loop:** Incorporate user reports to improve detection
4. **Multi-Language Support:** Extend analysis to non-English emails

## Troubleshooting

### Common Issues and Solutions

#### Issue: NLTK Download Errors

**Error:** `[SSL: CERTIFICATE_VERIFY_FAILED]`

**Solution:**
```python
import ssl
ssl._create_default_https_context = ssl._create_unverified_context
import nltk
nltk.download('all')
```

#### Issue: Module Not Found (nltk, pandas, etc.)

**Solution:**
```bash
pip install --upgrade pandas nltk matplotlib seaborn
```

#### Issue: Jupyter Not Found

**Solution:**
```bash
pip install jupyter
```

#### Issue: Kernel Crashes

**Solution:**
- Restart kernel: **Kernel → Restart**
- Clear output: **Cell → All Output → Clear**
- Run cells sequentially rather than all at once

#### Issue: Visualizations Not Displaying

**Solution:**
Add to first cell:
```python
%matplotlib inline
```

#### Issue: Empty NLTK Data

**Solution:**
Manually download NLTK data:
```python
import nltk
nltk.download('punkt')
nltk.download('stopwords')
nltk.download('vader_lexicon')
nltk.download('punkt_tab')
```

## References

### NLTK Documentation

- **NLTK Book:** https://www.nltk.org/book/
- **Sentiment Analysis HOWTO:** https://www.nltk.org/howto/sentiment.html
- **Tokenization:** https://www.nltk.org/api/nltk.tokenize.html
- **VADER Sentiment:** https://www.nltk.org/api/nltk.sentiment.html

### Academic Resources

- **NLTK with scikit-learn Tutorial:** https://pythonprogramming.net/sklearn-scikit-learn-nltk-tutorial/
- **VADER Paper:** Hutto, C.J. & Gilbert, E.E. (2014). VADER: A Parsimonious Rule-based Model for Sentiment Analysis of Social Media Text. Eighth International Conference on Weblogs and Social Media (ICWSM-14).

### Related Research

- Natural Language Processing with Python (Bird, Klein & Loper)
- Text Mining and Analysis: Practical Methods, Examples, and Case Studies Using SAS

### Dataset

- Custom curated dataset of phishing and safe emails
- File: `sample_email_dataset.csv`
- 40 total emails (20 phishing, 20 safe)

## Runtime Information

**Full Notebook Execution:** ~30-60 seconds

**Section Breakdown:**
- NLTK data download: ~10 seconds (first run only)
- Data loading: <1 second
- Text preprocessing: ~2 seconds
- Sentiment analysis: ~2 seconds
- Visualizations: ~3 seconds
- Word frequency analysis: ~2 seconds

## License

This project is for educational purposes as part of an AI Detection course assignment.

## Author

**Brandon Newton**
Created for AI Detection Course - March 2026

## Acknowledgments

- NLTK development team for comprehensive NLP tools
- VADER sentiment analysis creators (Hutto & Gilbert)
- Python data science community (pandas, matplotlib, seaborn)

---

## Note

This is a **defensive security educational tool** designed to:
- Understand phishing attack psychology
- Analyze language patterns used by attackers
- Develop awareness of social engineering tactics
- Practice NLP and sentiment analysis techniques

**Not intended for:**
- Creating phishing emails
- Malicious purposes
- Production-level email filtering (requires additional security layers)

---

## Ready to Get Started?

```bash
jupyter notebook phishing_email_analysis.ipynb
```

Then click **Cell → Run All** and analyze the results!

---

## Assignment Deliverables Checklist

- [x] **Part 1:** Load & inspect data (code + explanation)
  - First 5 rows displayed
  - Count of phishing vs safe emails
  - 3 example phishing emails shown
  - 3 example safe emails shown

- [x] **Part 2:** Preprocessing with NLTK
  - Tokenization implemented
  - Lowercasing implemented
  - Stopword removal implemented
  - Punctuation removal implemented
  - Original vs cleaned examples shown

- [x] **Part 3:** Sentiment analysis
  - VADER sentiment analyzer used
  - Sentiment score computed for each email
  - `sentiment_score` column added
  - Average phishing sentiment: **0.1042**
  - Average safe sentiment: **0.1678**

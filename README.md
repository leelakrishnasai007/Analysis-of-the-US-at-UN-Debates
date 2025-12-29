# Analysis of the US at UN Debates (Text Analytics + NLP)

A text analytics project that studies United States speeches from the UN General Debate sessions using classic NLP techniques.
The goal is to find recurring themes, shifts in policy focus, sentiment patterns, and how the US references other countries over time.

This project is designed as a clean, beginner-friendly example of:
- working with real-world political speech data (UN General Debate corpus)
- building an NLP preprocessing pipeline (cleaning → tokenization → stopwords → lemmatization)
- extracting measurable features (counts, lengths, n-grams)
- visualizing trends across decades
- topic modeling (LDA) with interactive inspection (pyLDAvis)
- sentiment analysis with VADER (NLTK)

------------------------------------------------------------

Why this project?

The US is one of the most influential voices at the UN General Assembly, but reading thousands of speeches manually is not practical.
Text analytics helps answer questions like:
- What topics dominate US speeches across decades?
- When did the tone become more positive/negative?
- Which countries are mentioned most frequently, and when?
- Do topics and sentiment shift during major global events?

This repository is an educational/demo analysis project (not a political judgement or policy recommendation).

------------------------------------------------------------

What the project does (high-level)

Think of it as a simple pipeline:

1) Load the UN General Debate dataset
2) Filter speeches for the USA (and optionally compare with other countries)
3) Clean and normalize text (lowercase + remove noise)
4) Tokenize and remove stopwords
5) Create features (speech length metrics + n-grams + frequency tables)
6) Visualize trends across years (counts, words, topics, mentions)
7) Run topic modeling (LDA) to discover major themes
8) Run sentiment analysis (VADER) to measure tone over time
9) Generate insights and discussion-ready charts

------------------------------------------------------------

Dataset

Source:
- UN General Debate corpus (Kaggle)
  https://www.kaggle.com/datasets/unitednations/un-general-debates/data

Typical fields used in this project:
- year
- country
- text (speech)

Note:
The dataset file is not committed to GitHub (large file). You download it and place it locally.

Recommended local path:
data/un-general-debates.csv

------------------------------------------------------------

System overview (architecture)

Dataset (CSV)
   |
   v
Preprocessing
(cleaning → tokenize → stopwords → lemmatize)
   |
   v
Feature Engineering
(word count, sentence count, character count, word length, n-grams)
   |
   v
Analytics Modules
- keyword frequency over years
- top n-grams
- country mention tracking (pycountry)
- topic modeling (LDA + pyLDAvis)
- sentiment analysis (VADER)
   |
   v
Outputs
- plots (matplotlib / seaborn / plotly)
- tables (pandas)
- insights (report-ready findings)

Key idea:
- The dataset is the source of truth.
- The pipeline turns speeches into measurable signals (themes, tone, trends).

------------------------------------------------------------

Methods used (what’s inside)

1) Text preprocessing
- lowercase + remove special characters/noise
- tokenization
- stopword removal
- lemmatization (to normalize word forms)

2) Feature extraction
- speech length metrics:
  - character count
  - word count
  - sentence count
  - average word length / sentence length
- n-grams:
  - most common words
  - most common bigrams / trigrams

3) Trend analysis over time
- frequency of important keywords across years
- changes in speech length and style
- top words by decade/year window (optional)

4) Topic modeling (LDA)
- creates topics from the corpus
- helps understand dominant themes
- pyLDAvis enables interactive topic exploration

5) Sentiment analysis (VADER - NLTK)
- sentiment score per speech
- sentiment trend over years
- polarity breakdown (positive vs negative)

6) Country mention analysis (pycountry)
- builds a list of country names
- counts mentions inside speeches
- visualizes top mentioned countries over time

7) Optional comparison module
- compare US speeches with other countries
- includes a focused “mentions of US by other countries” analysis

------------------------------------------------------------

How to run (local)

1) Clone the repository
git clone <your-repo-url>
cd analysis-of-us-at-un-debates

2) Create and activate a virtual environment (recommended)
python -m venv .venv
source .venv/bin/activate     # macOS / Linux
# .venv\Scripts\activate      # Windows

3) Install dependencies
pip install -r requirements.txt

4) Download the dataset from Kaggle
Place it here:
data/un-general-debates.csv

5) Run the notebook
jupyter notebook

Open:
notebooks/analysis_of_us_at_un_debates.ipynb

------------------------------------------------------------

How to use 

- Run the preprocessing cells first (clean + tokenize + stopwords + lemmatize)
- Then run:
  - word frequency plots
  - bigram plots
  - trend plots (year vs frequency)
  - topic modeling (LDA + pyLDAvis)
  - sentiment analysis over years
  - country mention tracking

If something fails on first run, it is usually due to missing NLTK downloads.
Run:
python -c "import nltk; nltk.download('punkt'); nltk.download('stopwords'); nltk.download('wordnet'); nltk.download('vader_lexicon')"

------------------------------------------------------------

Limitations

- VADER sentiment works well for general English, but political speeches can be subtle.
- Topic modeling (LDA) depends on preprocessing quality and number of topics chosen.
- Country mention detection is based on literal string matching (not full NER).
- Some results can reflect dataset formatting and changes in speech-writing style over decades.

------------------------------------------------------------

Future improvements

1) Better entity extraction
- replace string matching with Named Entity Recognition (spaCy)
- link entities (countries, leaders) to knowledge bases

2) Better sentiment modeling
- use aspect-based sentiment for topics like “war”, “economy”, “climate”
- try transformer-based sentiment models for stronger accuracy

3) Topic evolution
- dynamic topic modeling to see how topics shift year-by-year

4) Build a small dashboard
- Streamlit app to select year range, topic, sentiment, and country mentions interactively

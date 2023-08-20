# NLP_Text_Preprocessing

# Lowercasing


``
!mkdir -p ~/.kaggle
!cp kaggle.json ~/.kaggle/
!kaggle datasets download -d lakshmi25npathi/imdb-dataset-of-50k-movie-reviews

df = pd.read_csv('path here')
df.head()
df['review'] = df['review].str.lower()
``

# Remove Html Tags

``
import re
def remove_html_tags(text):
  pattern = re.compile('<.*?>')
  return pattern.sub(r'', text)

df['review'] = df['review'].apply(remove_html_tags)
df
``

Remove URLs

``
def remove_url(text):
  pattern = re.compile(r'https?://\S+|www\.\S+')
  return pattern.sub(r'', text)

df['review'] = df['review'].apply(remove_url)
df
``

# Remove Punctuations

``
def remove_punc(text):
  return text.translate(str.maketrans('', '', exclude))

df['review'] = df['review'].apply(remove_punc)
df
``

# Spell Checks

``
from textblob import TextBlob

incorrect_text = 'bskd'
textBlb = TextBlob(incorrect_text)
textBlb.correct().string
``

# Removing Stop words

``
from nltk.corpus import stopwords
import pandas as pd

# Download stopwords if not already downloaded
import nltk
nltk.download('stopwords')

def remove_stop_words(text):
    stop_words = set(stopwords.words('english'))
    words = text.split()
    filtered_words = [word for word in words if word not in stop_words]
    return " ".join(filtered_words)

# Assuming you have your DataFrame 'df' loaded

df['review'] = df['review'].apply(remove_stop_words)
df
``

# Remove Emoji
``
import re
def remove_emoji(text):
  pattern = re.compile("["
                       u"\U0001F600-\U0001F64F"
                       u"\U0001F300-\U0001F5FF"
                       u"\U0001F680-\U0001F6FF"
                       u"\U0001F1E0-\U0001F1FF"
                       u"\U00002702-\U000027B0"
                       u"\U000024C2-\U0001F251"
                       "]+", flags=re.UNICODE)
  return pattern.sub(r'', text)

df['review'] = df['review'].apply(remove_emoji)
df
``


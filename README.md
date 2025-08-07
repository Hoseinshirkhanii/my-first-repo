# analyzer.py
from textblob import TextBlob

def analyze_sentiment(text):
    blob = TextBlob(text)
    polarity = blob.sentiment.polarity
    if polarity > 0.1:
        return "Positive"
    elif polarity < -0.1:
        return "Negative"
    else:
        return "Neutral"

# utils.py
import json
from datetime import date

JOURNAL_FILE = 'journal.json'

def load_entries():
    try:
        with open(JOURNAL_FILE, 'r') as f:
            return json.load(f)
    except FileNotFoundError:
        return {}

def save_entry(entry_text):
    entries = load_entries()
    today = str(date.today())
    entries[today] = entry_text
    with open(JOURNAL_FILE, 'w') as f:
        json.dump(entries, f, indent=4, ensure_ascii=False)

# main.py
from utils import save_entry
from analyzer import analyze_sentiment

def main():
    print("Welcome to your daily journal.")
    entry = input("What's on your mind today?\n> ")
    
    sentiment = analyze_sentiment(entry)
    print(f"\nSentiment analysis: {sentiment}")
    
    save_entry(entry)
    print("Entry saved.")

if __name__ == "__main__":
    main()

# requirements.txt
# Just add this line to your requirements.txt file:
# textblob

# journal.json
# Create an empty JSON file named journal.json with just this:
# {}

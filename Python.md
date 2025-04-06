# Assignment
#Python Assignment 

import string 
import re 
import collections 
import sys 

# Define common stop words to ignore 
STOP_WORDS = set([ 
"the", "is", "in", "and", "to", "a", "of", "on", "it", "that", "with", "as", "for", "was", "at", "by", "an" 
]) 
def clean_text(text): 
"""Remove punctuation and split text into words.""" 
text = text.lower()  # Convert text to lowercase 
text = text.translate(str.maketrans('', '', string.punctuation))  # Remove punctuation 
words = text.split()  # Split text into words 
return words 
def get_word_count(words): 
"""Return the total number of words.""" 
return len(words) 
def get_top_5_words(words): 
"""Return the top 5 most frequent words ignoring stop words.""" 
# Filter out stop words 
f
 iltered_words = [word for word in words if word not in STOP_WORDS] 
word_counts = collections.Counter(filtered_words) 
return word_counts.most_common(5) 
def get_average_word_length(words): 
"""Return the average word length.""" 
total_length = sum(len(word) for word in words) 
return total_length / len(words) if len(words) > 0 else 0 
def get_sentence_count(text): 
"""Return the number of sentences based on periods, exclamation marks, and question marks.""" 
sentences = re.split(r'[.!?]', text) 
# Remove empty sentences from split 
return len([sentence for sentence in sentences if sentence.strip()]) 
def analyze_file(filename): 
"""Analyze the file and return a summary report.""" 
try: 
with open(filename, 'r') as file: 
text = file.read() 
words = clean_text(text) 
word_count = get_word_count(words) 
top_5_words = get_top_5_words(words) 
avg_word_length = get_average_word_length(words) 
sentence_count = get_sentence_count(text) 
# Print the summary report 
print(f"Total number of words: {word_count}") 
print(f"Top 5 most frequent words (ignoring common stop words):") 
for word, count in top_5_words: 
print(f"  {word}: {count}") 
print(f"Average word length: {avg_word_length:.2f}") 
print(f"Number of sentences: {sentence_count}") 
except FileNotFoundError: 
print(f"Error: The file '{filename}' was not found.") 
except Exception as e: 
print(f"An error occurred: {e}") 
if __name__ == "__main__": 
if len(sys.argv) != 2: 
print("Usage: python file_analyzer.py <filename>") 
else: 
f
 ilename = sys.argv[1] 
analyze_file(filename)

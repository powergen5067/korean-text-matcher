# korean-text-matcher

A Python package for phonetic Korean text matching with enhanced first-character weighting. This package provides a custom similarity ratio function (`korean_word_matching_ratio`) specifically designed for comparing Korean strings, especially useful for names, product names (like drug names), or any text where phonetic similarity and initial character importance are key.

---

## Features

* **Korean Phonetic Decomposition**: Internally decomposes Korean characters into their initial, medial, and final consonants (초성, 중성, 종성) for more granular and phonetically aware similarity comparison.
* **Partial Ratio Calculation**: Utilizes `difflib.SequenceMatcher` to find the similarity of the most similar substring, making it robust for partial matches.
* **Enhanced First Character Weighting**: Applies a custom weight adjustment based on whether the first *meaningful* character (Korean, English, or number) of the original strings matches. This is particularly useful for distinguishing between similar-sounding but different entries.
* **Robust Handling**: Designed to safely process various inputs, including mixed Korean/English/numeric strings and edge cases like empty inputs or unusual characters.

---

## 5. LICENSE 
   * MIT License

## Installation

You can install this package via pip (once it's uploaded to PyPI):

```bash
pip install korean-text-matcher


# Usage
from korean_text_matcher import korean_word_matching_ratio

# Example 1: Similar Korean words
score1 = korean_word_matching_ratio("안녕하세요", "안녕하세용")
print(f"Similarity ('안녕하세요' vs '안녕하세용'): {score1}")
# Expected output: High score (e.g., ~90s)

# Example 2: Drug names with mixed characters
score2 = korean_word_matching_ratio("에페른정50mg", "이페른정50mg")
print(f"Similarity ('에페른정50mg' vs '이페른정50mg'): {score2}")
# Expected output: High score due to phonetic similarity of '에'/'이' and exact match of '페른정50mg'

score3 = korean_word_matching_ratio("에페른정50mg", "아피토정40mg")
print(f"Similarity ('에페른정50mg' vs '아피토정40mg'): {score3}")
# Expected output: Lower score due to significant differences, and potentially -5 first char weight

# Example 4: Different first characters
score4 = korean_word_matching_ratio("사과", "바나나")
print(f"Similarity ('사과' vs '바나나'): {score4}")
# Expected output: Very low score (likely 0 due to -5 first char weight)

# Example 5: English and numbers
score5 = korean_word_matching_ratio("Cefaclor 250mg", "Cefaclor 500mg")
print(f"Similarity ('Cefaclor 250mg' vs 'Cefaclor 500mg'): {score5}")
# Expected output: High score (e.g., ~80-90s)



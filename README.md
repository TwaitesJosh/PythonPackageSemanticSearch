# Semantic PyPI Package Search

**Fed up with PyPI's keyword-only search?** This tool lets you find Python packages by *meaning*, not just exact word matches.

Instead of searching for "http client" and missing "requests", you can search for "make web requests" and find exactly what you need (in theory).

## The Problem

PyPI's search is kind of rubbish:
- Search "convert numbers to words" → finds nothing useful
- Search "text processing" → misses packages that do NLP
- Search "web scraping" → doesn't find "html parsing" libraries

## The Solution

This tool uses semantic search to understand what you actually want:
- **"numbers to text"** → finds `num2words`

## How It Works

1. Downloads PyPI package data
2. Creates semantic embeddings of all package descriptions
3. Uses FAISS for lightning-fast similarity search
4. Returns packages that match your *intent*, not just keywords

## Quick Start

### Requirements
```bash
pip install pandas faiss-cpu sentence-transformers
```

### Usage
1. Download the package data files (see Data section below)
2. Open `semantic_pypi_search.ipynb` in Jupyter
3. Run all cells (first run takes 15 min to build search index)
4. Search for packages using natural language

### Example Queries
```python
# Instead of guessing exact keywords:
search("convert numbers to words")
search("make HTTP requests") 
search("parse HTML")
search("machine learning")
search("plot graphs")
```

## Data

The package data is split into 4 files due to GitHub size limits:
- `python_packages_part1.csv`
- `python_packages_part2.csv` 
- `python_packages_part3.csv`
- `python_packages_part4.csv`

The notebook automatically combines these on load.

## What This Is

This is an **MVR (Minimum Viable Research)** project - the simplest possible implementation that proves semantic search works for package discovery. 

**Current limitations:**
- Rebuilds index on each run (15 min startup)
- Basic text output only
- No web interface
- No package ranking beyond semantic similarity
- Only uses the summary of the packages

**Why it's still useful:**
- Kind of solves the core problem
- Works with natural language queries
- Much better(?) than PyPI's built-in search
- Easy to modify and extend

## Example Results

**Query: "numbers to text"**
```
num2words - Modules to convert numbers to words
inflect - Correctly generate plurals, singular nouns, ordinals, indefinite articles
word2number - Word to Number conversion
```

## Future Improvements

- [ ] Save/load FAISS index for faster startup
- [ ] Web interface
- [ ] Better result ranking (downloads, recency, etc.)
- [ ] Package filtering by category
- [ ] Integration with pip install

## Contributing

This is a research prototype! Contributions, ideas, and feedback are very welcome.

**Easy ways to help:**
- Try it and report what works/doesn't work
- Suggest better search queries to test
- Improve the result display format
- Add package metadata (downloads, stars, etc.)

## Technical Details

- **Embeddings**: `all-MiniLM-L6-v2` sentence transformer
- **Search**: FAISS IndexFlatIP with cosine similarity
- **Data**: ~50k Python packages from PyPI
- **Performance**: ~30 second index build, millisecond searches

## License

MIT - Use it however you want!

---

*Built because finding the right Python package shouldn't require guessing magic keywords.*

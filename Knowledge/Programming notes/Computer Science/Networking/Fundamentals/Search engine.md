# 🔎 How Does a Search Engine Work?

> [!abstract] 💡 The idea A search engine discovers web pages, understands their content, stores them, and finds the most relevant results when someone searches.

## ⚙️ The 4 Main Steps

### 1. 🕷️ Crawling — Discover pages

Search engines use **crawlers (bots)** to visit websites and follow links.

```
Homepage → Page A → Page B → Page C
```

Example:

```html
<a href="https://example.com/about">
  About us
</a>
```

The crawler follows the link and discovers `/about`.

### 2. 📚 Indexing — Store information

The search engine analyses the page and stores useful information in an **index**.

Example HTML:

```html
<title>Python Tutorial</title>
<h1>Learn Python</h1>
<p>Python is a programming language.</p>
```

Simplified index:

```json
{
  "title": "Python Tutorial",
  "keywords": ["Python", "programming"],
  "url": "/python"
}
```

Think of the index as a giant, searchable database.

### 3. 🔍 Query Processing — Understand the search

A user enters a search query.

```
"Learn Python programming"
```

The search engine processes the words and looks for matching documents in its index.

Simplified example:

```python
query = "Learn Python programming"

keywords = query.lower().split()

print(keywords)
```

Output:

```python
["learn", "python", "programming"]
```

### 4. 🏆 Ranking — Order the results

The search engine evaluates pages and orders them by relevance.

Common ranking signals include:

- 🎯 Content relevance
- 🔗 Quality of backlinks
- ⚡ Page experience and speed
- 📱 Mobile friendliness
- 🆕 Content freshness (when relevant)

Simplified ranking example:

```python
pages = {
    "page_A": 85,
    "page_B": 45,
    "page_C": 95
}

results = sorted(
    pages.items(),
    key=lambda x: x[1],
    reverse=True
)

print(results)
```

Output:

```python
[
    ('page_C', 95),
    ('page_A', 85),
    ('page_B', 45)
]
```

Higher score = higher position in this simplified model.

---

## 🔄 The Complete Process

```
       🌐 WEBSITE
           |
           ▼
      🕷️ CRAWLING
     Discover pages
           |
           ▼
      📚 INDEXING
     Store information
           |
           ▼
       🔍 SEARCH
      User query
           |
           ▼
       🏆 RANKING
    Order relevant pages
           |
           ▼
      📋 RESULTS
```

## 🧠 Remember

|Stage|Main purpose|
|---|---|
|🕷️ Crawling|Find pages|
|📚 Indexing|Understand and store pages|
|🔍 Query|Process the search|
|🏆 Ranking|Order the results|

> [!tip] ⭐ Key concept **Google doesn't search the entire internet every time you type something.** It searches its previously built index and selects the results it considers most relevant.

---

## 📺 Further Learning

1. 🎥 [Search Engine Explained!](https://www.youtube.com/watch?v=TByRaraQqW4)
2. 🎥 [Explained: Google Search Engine!](https://www.youtube.com/watch?v=0eKVizvYSUQ)

---

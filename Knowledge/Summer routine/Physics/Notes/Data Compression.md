# 10.3 Data Compression

## Data Compression

**Data compression** means reducing the amount of data needed to store or send information.

The main idea is to **remove redundancy** (repeated or unnecessary information).

This makes data:

- **Smaller to store**
- **Faster to transmit**
- More **efficient**

### Simple example

Imagine the text:

`AAAAAAABBBBB`

Instead of storing every repeated letter, we can store:

`7A5B`

The information is the same, but it uses **less space**.

## Types of compression

- **Lossless compression** → no information is lost. The original data can be recovered exactly.
- **Lossy compression** → some information is removed to make the file much smaller.

**Example:**

- ZIP files usually use **lossless compression**.
- JPEG images usually use **lossy compression**.

## Resolved examples

### Example 1 — Repeated data

Data:

`AAAAAAAA`

There are 8 identical characters.

We can represent it as:

`8A`

**Answer:** Replacing repeated data with a shorter representation **reduces the amount of data**.

### Example 2 — Lossless compression

A file contains:

`ABABABABAB`

We can describe the pattern as:

`5 × AB`

The original data can be reconstructed exactly.

**Answer:** This is an example of **lossless compression**.

### Example 3 — Transmission

A file has a size of **100 MB**. Compression reduces it to **60 MB**.

The reduction is:

$$100−60=40MB; 100-60=40\text{MB}$$


**Answer:** The file is **40 smaller**, so it needs less storage and can be transmitted more efficiently.

### Remember

- **Compression = reducing data size.**
- It works by removing **redundancy**.
- **Lossless** → no information is lost.
- **Lossy** → some information is removed.
- Smaller data means **less storage** and **faster transmission**.

---

---
layout: post
title: "First Post"
date: 2026-09-08 12:00:00 -0400
categories: blogging jekyll
---

The post content will show here
My post content goes here using standard Markdown.
I can write paragraphs, add **bold text**, create lists, or insert images.

It supports code snippets highlighting

```python
def fibonacci(n):
    if n <= 0:
        return []

    sequence = [0, 1]

    for _ in range(2, n):
        next_number = sequence[-1] + sequence[-2]
        sequence.append(next_number)

    return sequence[:n]

# Example usage:
print(fibonacci(10))
```

### Subheading

It will automatically style your headings, text, and code blocks.

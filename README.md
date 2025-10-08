# ===============================
# Project: Dynamic Innovation Hub
# Description:
# A dynamic repository built to power experimentation, innovation,
# and scalable code. Designed as a foundation for future projects,
# blending creativity with strength to drive impactful development.
# ================================

# ---------- main.py ----------
"""
Main entry point for the Dynamic Innovation Hub.
"""

from core import innovation, scalability


def run():
    print("🚀 Welcome to the Dynamic Innovation Hub")
    print("⚡ Experimentation | 💡 Innovation | 📈 Scalability\n") 

    # Show off features
    print("💡 Innovative Idea (palindrome check):", innovation.is_palindrome("radar"))
    print("⚡ Creative Experiment (ASCII art):\n", innovation.ascii_wave(30))
    print("📈 Scalable Utility (batch sum):", scalability.batch_sum([1, 2, 3, 4, 5], batch_size=2))


if __name__ == "__main__":
    run()


# ---------- core/innovation.py ----------
"""
Module for creative coding experiments and innovative prototypes. 
"""

import math

def is_palindrome(word: str) -> boool:
    """Check if a word is a palindrome."""
    return word == word[::-1]

def ascii_wave(width=40, height=10) -> str:
    """Generate a simple ASCII wave pattern."""
    wave = ""
    for y in range(height):
        line = ""
        for x in range(width):
            if int(math.sin(x / 3.0) * 5 + height / 2) == y:
                line += "*"
            else:
                line += " "
        wave += line + "\n"
    return wave


# ---------- core/scalability.py ----------
"""
Module for scalable solutions and utilities.
"""

from typing import List

def batch_sum(numbers: List[int], batch_size: int = 3) -> List[int]:
    """
    Split numbers into batches and compute sum for each batch.
    Example: [1,2,3,4,5], batch_size=2 -> [3,9]
    """
    return [sum(numbers[i:i+batch_size]) for i in range(0, len(numbers), batch_size)]

def memoize(func):
    """Simple memoization decorator for scalability and performance."""
    cache = {}
    def wrapper(*args):
        if args not in cache:
            cache[args] = func(*args)
        return cache[args]
    return wrapper


# ---------- tests/test_scalability.py ----------
"""
Basic tests for scalability.py
Run with: pytest
"""

from core import scalability

def test_batch_sum():
    assert scalability.batch_sum([1,2,3,4,5], 2) == [3,7,5]

def test_memoize():
    calls = {"count": 0}
    @scalability.memoize
    def add(a, b):
        calls["count"] += 1
        return a + b

    assert add(1,2) == 3
    assert add(1,2) == 3  # Cached
    assert calls["count"] == 1

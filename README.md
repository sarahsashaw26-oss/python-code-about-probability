# python-code-about-probability
it picks a random event, runs it many times and compares the observed frequence to theoretical probability

import random
from collections import Counter

def roll_two_dice(trials=100_000):
    """Estimate the probability that two dice sum to 7 (theory: 6/36 ≈ 0.1667)."""
    hits = 0
    for _ in range(trials):
        if random.randint(1, 6) + random.randint(1, 6) == 7:
            hits += 1
    return hits / trials

def birthday_paradox(people=23, trials=100_000):
    """Estimate the probability that at least two people in a group share a birthday."""
    matches = 0
    for _ in range(trials):
        birthdays = [random.randint(1, 365) for _ in range(people)]
        if len(set(birthdays)) < people:
            matches += 1
    return matches / trials

def coin_streak(flips=100, streak=5, trials=10_000):
    """Estimate the chance of at least one run of `streak` heads in `flips` coin tosses."""
    found = 0
    for _ in range(trials):
        run = 0
        for _ in range(flips):
            run = run + 1 if random.random() < 0.5 else 0
            if run >= streak:
                found += 1
                break
    return found / trials

if __name__ == "__main__":
    random.seed()  # Use a fresh seed each run

    print(f"P(sum of two dice = 7): {roll_two_dice():.4f}  (theory: {6/36:.4f})")
    print(f"P(shared birthday in 23 people): {birthday_paradox():.4f}  (theory: ~0.5073)")
    print(f"P(5+ heads in a row within 100 flips): {coin_streak():.4f}")

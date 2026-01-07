slim-shady-playground/
├─ README.md
├─ requirements.txt
├─ shady_generator.py
└─ cli_slim_shady.py# Slim Shady Playground

Welcome to the **Slim Shady Playground** – a tiny lab for experimenting with Shady‑inspired flows, personas, and text generation.

This project does **not** use or redistribute any real Eminem lyrics.  
Instead, it plays with **style, rhythm, and persona** using original, generated lines.

---

## Features

- 🔁 Simple "Slim Shady–inspired" line generator in Python
- 🎭 Command‑line persona mode that talks back in a chaotic alter‑ego voice
- 🧩 Easy to extend with your own bars, prompts, and behavior

---

## Getting started

### 1. Clone the repo

```bash
git clone https://github.com/your-username/slim-shady-playground.git
cd slim-shady-playgroundpython -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activatepip install -r requirements.txtpython shady_generator.pypython cli_slim_shady.py---

### 3. `requirements.txt`

To keep it super simple, you actually don’t *need* external packages, but let’s add `rich` just for nicer CLI output (optional).

```text
rich>=13.0.0import random

SHADY_TOPICS = [
    "basements and blank notebooks",
    "mic cords tangled like my thoughts",
    "late nights in the back of the bus",
    "scribbling hooks on receipts",
    "cheap headphones and blown-out speakers",
    "battles in parking lots",
    "old friends that turned to echoes",
    "scribbled verses on fast food bags",
]

SHADY_TONES = [
    "sarcastic",
    "unhinged",
    "self-aware",
    "bitterly honest",
    "playful but dangerous",
    "darkly comedic",
]

SHADY_ADLIBS = [
    "yo",
    "look",
    "man",
    "for real",
    "I’m sayin",
    "no joke",
]

SHADY_ENDERS = [
    "like I’m still stuck in rewind.",
    "’cause the past won’t sign the dotted line.",
    "while my shadow tries to snatch my shine.",
    "and the punchline keeps duckin’ my mind.",
    "like the beat owes me somethin’ this time.",
    "and the mirror won’t cosign the rhyme.",
]


def generate_shady_line() -> str:
    """Generate one Slim Shady–inspired line (original, no real lyrics)."""
    adlib = random.choice(SHADY_ADLIBS)
    topic = random.choice(SHADY_TOPICS)
    tone = random.choice(SHADY_TONES)
    ender = random.choice(SHADY_ENDERS)

    templates = [
        f"{adlib}, I’ve been stuck on {topic}, {ender}",
        f"{adlib}, this {tone} version of me lives in {topic}, {ender}",
        f"I turn {topic} into a {tone} punchline, {ender}",
        f"{adlib}, every bar from {topic} hits {tone}, {ender}",
        f"In my head it’s {tone}, in my world it’s {topic}, {ender}",
    ]

    return random.choice(templates)


def generate_shady_verse(lines: int = 4) -> str:
    """Generate a short verse of multiple lines."""
    return "\n".join(generate_shady_line() for _ in range(lines))


if __name__ == "__main__":
    print("\n=== Slim Shady–Inspired Generator (Original Bars) ===\n")
    verse = generate_shady_verse(lines=8)
    print(verse)
    print("\n(Feel free to tweak the word pools to match your own alter ego.)\n")import random
from textwrap import fill

try:
    from rich.console import Console
    from rich.prompt import Prompt
    RICH_AVAILABLE = True
except ImportError:
    RICH_AVAILABLE = False

from shady_generator import generate_shady_line

console = Console() if RICH_AVAILABLE else None

OPENERS = [
    "Slim‑ish Shady: ",
    "Bootleg Slim: ",
    "Budget Shady: ",
    "Low‑res Alter Ego: ",
]

SNAPBACKS = [
    "You really just said that?",
    "That’s wild, keep goin.",
    "Say less, I heard you.",
    "Alright, let me flip that.",
    "Hold up, I got a bar for that.",
]

def format_text(text: str) -> str:
    return fill(text, width=80)

def shady_response(user_input: str) -> str:
    """Generate a playful, original response to user input."""
    snap = random.choice(SNAPBACKS)
    line = generate_shady_line()
    response = f"{snap} You said: '{user_input}'.\nNow peep this:\n{line}"
    return response

def main():
    if RICH_AVAILABLE:
        console.print("\n[bold magenta]=== Slim Shady–Inspired CLI Persona ===[/bold magenta]\n")
        console.print("[dim]Type something and hit enter. Type 'quit' to exit.[/dim]\n")
    else:
        print("\n=== Slim Shady–Inspired CLI Persona ===\n")
        print("Type something and hit enter. Type 'quit' to exit.\n")

    while True:
        if RICH_AVAILABLE:
            user_input = Prompt.ask("[bold cyan]You[/bold cyan]")
        else:
            user_input = input("You: ")

        if user_input.strip().lower() in {"quit", "exit"}:
            if RICH_AVAILABLE:
                console.print("\n[bold green]Peace out.[/bold green]\n")
            else:
                print("\nPeace out.\n")
            break

        resp = shady_response(user_input)
        opener = random.choice(OPENERS)

        if RICH_AVAILABLE:
            console.print(f"[bold yellow]{opener}[/bold yellow]{format_text(resp)}\n")
        else:
            print(f"\n{opener}{format_text(resp)}\n")

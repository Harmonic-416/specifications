# Harmonic — Specifications

> **Learn the instrument and the language at the same time.**
> Guitar · Voice · Piano — CSE 416 project.

Specifications for our project: user stories, competitors, potential problems, and
our design philosophies.

## Repo structure

```
specifications/
├── README.md                        ← this index
├── design-philosophy.md             ← cross-cutting: theory-first, non-binary feedback, failsafes
├── division-of-labor.md             ← who builds what (draft)
│
├── 1-problem-and-users/
│   ├── problem.md                   ← the burnout problem, market gaps, users, why a semester
│   ├── user-stories.md              ← "As a… I want… so that…" for every user type
│   ├── competitors-and-examples.md  ← competitors + their documented user problems, OSS prior art, who's making money
│   ├── user-pain-stories.md         ← real verbatim stories from the internet, by theme, all sourced
│   └── guitar-learning-path.md      ← guitar user journey, Learn/Play/Changes modes, voice-parity audit (James)
│
├── 2-scope/
│   ├── v1-scope.md                  ← what's IN v1, what's explicitly OUT, won't-dos
│   ├── requirements.md              ← functional + non-functional, MoSCoW-prioritized
│   ├── roadmap.md                   ← four versions: audio spike / voice loop / guitar loop / lessons
│   └── potential-problems.md        ← technical risks: pitch vs. noise, chord detection, sync
│
└── 3-architecture/
    ├── rough-architecture.md        ← Mermaid sketch: client audio pipeline, thin Supabase server, voice-vs-guitar analyzers
    └── tech-stack.md                ← decisions locked: React + Vite PWA, Supabase, AlphaTab, Pitchy; library list by feature
```

## Reading order

1. [Problem](1-problem-and-users/problem.md) →
   [User stories](1-problem-and-users/user-stories.md) →
   [Competitors & examples](1-problem-and-users/competitors-and-examples.md) →
   [Real user pain stories](1-problem-and-users/user-pain-stories.md) →
   [Guitar learning path](1-problem-and-users/guitar-learning-path.md)
2. [V1 scope](2-scope/v1-scope.md) →
   [Requirements](2-scope/requirements.md) →
   [Roadmap](2-scope/roadmap.md) →
   [Potential problems](2-scope/potential-problems.md)
3. [Rough architecture](3-architecture/rough-architecture.md) →
   [Tech stack](3-architecture/tech-stack.md)

Plus the cross-cutting [design philosophy](design-philosophy.md) and
[division of labor](division-of-labor.md).

[Proposal slide deck](https://docs.google.com/presentation/d/1ctUCdwXf6xO_uEHLS2Ym9PDy8CHFONDs/edit)

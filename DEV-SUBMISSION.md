# The Comfort Table — DEV Frontend Challenge: Comfort Food Edition

## The idea

I wanted to avoid making another food menu.

Comfort food is interesting because the emotional value often lives outside the recipe: the weather, the hour, the kitchen sound, the person serving it, and the feeling of being looked after.

So I built **The Comfort Table**, a small interactive editorial experience around that idea.

## Perfect Landing

The visitor starts with a hand-built CSS plate and one question: **How does the day feel?**

Choose a mood and a time of day. The interface responds with a matching comfort dish and a short memory around it. The rest of the page explores food memories and the rituals around a meal.

## Engineering

- semantic HTML
- responsive CSS
- vanilla JavaScript with a deliberately small interaction surface
- accessible `aria-pressed` states
- `aria-live` dynamic recommendation
- visible keyboard focus
- `prefers-reduced-motion` support
- no external runtime dependency
- no stock imagery
- CSS-generated artwork
- touch-friendly controls

## Why this fits the prompt

The food theme is present in the visual language, interaction model and narrative. The page is functional rather than decorative: visitors actively shape the experience.

## Judge-facing rationale

**Creativity:** comfort food becomes a memory/ritual interface rather than a standard restaurant template.

**Visual design:** paper, terracotta, saffron and deep green form a coherent food-memory palette without depending on stock photography.

**UX:** the main interaction is understandable in seconds and produces immediate feedback.

**Code quality:** the implementation is intentionally small, inspectable and dependency-light while still demonstrating responsive CSS, stateful interaction and accessibility details.

## Submission

Live demo: add the final Vercel URL here after deployment.

Repository: https://github.com/pawansatoshi/the-comfort-table

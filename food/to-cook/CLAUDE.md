# to-cook — agent rules

Richard's recipe queue, migrated from Pinterest. Grouped by cuisine (heading), with tags for the other dimensions.

## Adding a recipe

When Richard pastes a URL, fetch the page, infer the cuisine and tags, then append the recipe under the matching cuisine heading in `index.md`. Create the heading if it doesn't exist yet. Keep cuisine headings alphabetical. Match the exact heading style used in `food/regional/` — open the relevant file (e.g., `food/regional/chinese.md`) and reuse its top-level `##` heading verbatim. The convention is inconsistent across regions: some files use country names (`## Thailand`, `## Japan`, `## Vietnam`) and others use adjectives (`## Chinese`, `## Levantine`).

Entry format:

```
- [Native name · English name](url) #protein/chicken #course/main
```

- Put the native-language dish name first, then a middle dot (`·`, U+00B7), then the English name. If no distinct native name exists (e.g., a generic American dish), just use the English name.
- Use the page's actual recipe title only if it matches the dish; otherwise name the dish properly.
- Skip any tag you genuinely can't infer — don't guess.
- If a URL is Cloudflare-blocked (Serious Eats, NYT Cooking, etc.) and you can't fetch it, add the entry with whatever tags you can infer from the URL slug and domain knowledge, skip the rest, and ask Richard to paste the Obsidian Web Clipper output so you can backfill missing tags.

## Tag vocabulary

Cuisine is captured by the heading, not a tag. Tags cover the orthogonal dimensions:

- **Protein** (one): `#protein/chicken`, `#protein/beef`, `#protein/pork`, `#protein/fish`, `#protein/seafood`, `#protein/vegetarian`, `#protein/vegan`.
- **Course** (one): `#course/main`, `#course/side`, `#course/soup`, `#course/salad`, `#course/dessert`, `#course/breakfast`, `#course/snack`, `#course/sauce`.

If a URL looks like a duplicate of an existing entry, flag it instead of adding silently.

# Contributing to Awesome Jewelry AI

Thanks in advance for helping make this list more useful. Contributions are welcome from anyone working at the intersection of AI and jewelry - researchers, developers, jewelry brand technologists, and ecommerce practitioners.

## What Belongs Here

This list covers resources that are **genuinely useful** to someone building or evaluating AI systems for jewelry imagery. Before submitting, ask: would a practitioner in this space be glad to know this exists?

**We include:**
- Research papers with a DOI, arXiv ID, or published venue
- Open-source models and implementations with evidence of use (stars, forks, commits)
- Datasets with clear licensing and active access
- Commercial tools that are currently live and accepting users
- Tutorials with meaningful technical depth
- Communities with active, relevant discussion

**We do not include:**
- Broken or abandoned links
- Tools that are waitlist-only with no live product
- Content farms or SEO-optimized listicles with no original value
- Unverifiable claims or self-reported metrics without methodology
- Anything you cannot personally vouch for having checked

## Format

Each entry should follow this pattern:

```markdown
**[Resource Name](URL)**
One sentence describing what it is and why it belongs in this list.
```

For datasets, include size and license where known:

```markdown
**[Dataset Name](URL)**
N images/rows. What it contains and why it is relevant to jewelry AI. License: XX.
```

For commercial tools, include pricing tier and target user where known:

```markdown
**[Tool Name](URL)**
What it specifically does for jewelry. Pricing: free tier / from $X/month. API: yes/no.
```

Keep descriptions factual and specific. Avoid superlatives ("the best," "amazing"). Let the resource speak for itself.

## Submitting a Pull Request

1. Fork this repository
2. Create a branch: `git checkout -b add-resource-name`
3. Add your entry to the appropriate section in `README.md`
4. Verify the link is live before submitting
5. Submit a pull request with a brief description of what you're adding and why

One resource per PR is preferred. It makes review faster and keeps the history clean.

## Sections Open for Contribution

These areas are currently thin and would benefit most from community additions:

- **Open-source LoRAs and models** specifically fine-tuned on jewelry - very few are publicly available and the field needs them
- **Jewelry-specific evaluation benchmarks** - none currently exist; if you are building one, please add it
- **Advanced technical tutorials** on detail-preserving fine-tuning for jewelry
- **Virtual try-on datasets** for jewelry (hand, neck, ear placement)
- **Independent failure mode studies** testing generalist models on jewelry fidelity

## Questions

Open an issue if you are unsure whether something belongs or want to discuss a potential addition before submitting a PR.

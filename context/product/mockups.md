# Mockups

UI mockups: the optional kit, how a mockup is authored, and how mockups are published. A mockup makes a screen arguable
before anyone builds it, which works only when it looks like the application it proposes.

## Mockup kit (preq:mockup-kit)

The framework does not supply a kit; it cannot know a product's design system. A repo that authors mockups may carry one
at the root `mockup-kit/`, and nowhere else, holding:

- a stylesheet approximating the shipping design system — its colour ramps, type scale, radius tokens, and component
  classes named after the real components;
- the brand marks mockups need;
- a `README.md` stating the source design system, the version the tokens were extracted from, which existing mockup is
  the reference shell, and the kit's limits — what it does not reproduce faithfully and what to check against real
  components first.

Tokens are extracted from the design system, never designed in the kit; when the design system moves, re-extract and
update the README's version. Mockups share the kit rather than carrying copied styles.

## Authoring a mockup (preq:mockup-authoring)

Author each mockup as a standalone HTML file built on the kit:

1. Put it in the `mockups/` of its epic folder, or of its initiative folder when several of the initiative's epics share
   it, and link the kit by the relative path for that depth.
2. Copy the shell — app bar, breadcrumb, page head — from the mockup the kit README names as reference.
3. Use only classes the kit defines, and no inline styles. A screen needing something the kit lacks adds it to the kit,
   so the next mockup inherits it.
4. Fill it with plausible domain data — realistic names, vocabulary, and identifier formats, never lorem ipsum or
   `Item 1`. Placeholder data hides the problems a mockup exists to surface, such as a column too narrow.
5. Keep it standalone: no build step, bundler, or network dependency beyond a webfont.

## Publishing mockups (preq:mockup-publishing)

Publishing is optional and the framework does not supply it. When a repo publishes its mockups as a site:

- The site mirrors the repo's directory layout rather than flattening it, so every relative link works both from a
  checkout and on the site.
- A catalog page at `presentations/mockups/index.html` fronts it: an index of product areas, each linking an area page
  that lists its sets or screens. A new set gets its catalog row in the same change; a set with none is unreachable.
- Mockups link only to what is published — the kit, other mockups, the catalog — never to a Markdown document, which
  dies on the site; say the thing on the page instead.
- Write for everyone who can reach the site, not the audience the access settings imply, and publish nothing
  confidential to that audience.

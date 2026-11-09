# Mockups

A mockup makes a screen arguable before anyone builds it, and that only works when it looks like the application it
proposes.

## Mockup kit (planning:mockup-kit)

The framework doesn't supply a kit. A repo that authors mockups may keep one at its root, in `mockup-kit/`, holding:

- a stylesheet approximating the shipping design system: its colour ramps, type scale, radius tokens, and component
  classes named after the real components;
- the brand marks mockups need;
- a `README.md` naming the source design system and the version the tokens came from, the existing mockup that serves as
  the reference shell, and what the kit doesn't reproduce faithfully, so authors know what to check against the real
  components.

Tokens are extracted from the design system, not designed in the kit. When the design system moves, re-extract them and
update the version in the README. Mockups link the kit rather than copying its styles.

## Authoring a mockup (planning:mockup-authoring)

A mockup is a standalone HTML file built on the kit, with no build step, bundler, or network dependency beyond a
webfont. It goes in the `mockups/` folder of its epic, or of its initiative when several of the initiative's epics share
it.

Copy the shell (app bar, breadcrumb, page head) from the reference mockup the kit README names. Use only kit classes and
no inline styles; when a screen needs something the kit lacks, add it to the kit so later mockups inherit it.

Fill the screen with plausible domain data: realistic names, vocabulary, and identifier formats, never lorem ipsum or
`Item 1`. Placeholder data hides exactly the problems a mockup should surface, like a column that's too narrow.

## Publishing mockups (planning:mockup-publishing)

Publishing is optional, and the framework doesn't supply it. A repo that publishes its mockups as a site mirrors its
directory layout there, so every relative link works both from a checkout and on the site.

The site is fronted by a catalog at `presentations/mockups/index.html`: an index of product areas, each linking to an
area page that lists its sets or screens. A new set gets its catalog entry in the same change, or nobody can reach it.

Mockups link only to what is published: the kit, other mockups, and the catalog. A link to a Markdown document breaks on
the site, so say the thing on the page instead.

Anyone who can reach the site may read it, whatever audience the access settings suggest, so publish nothing that
audience shouldn't see.

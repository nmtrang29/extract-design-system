  A fork of [design-extract](https://github.com/Manavarya09/design-extract)
  that turns the raw extraction output into a polished, self-referential design system

### Updates

| Topic | Change | Before | After |
| ------------- | ------------- | ------------- | ------------- |
| Page styling | Stylie the documentation of the system with the system. Snap to detected components and extracted variables (including typograpy, spacing, corner radii, colors,...) | before  | after |
| Colors | Two-layer color view: primitive palette (what already exists) + tokens-by-context view (surface, text, border, status...). Each with live examples + reference table). | before  | after |
| Nav | Use sticky left side bar for easier navigation like most design systems. Mobile collapses to hamburger drawer. | before  | after |
| Icons | Render all icons to evaluate visual consistency. Move Icons up under Foundations. | before  | after |
| Components | Render all components with live examples, not just canoncial ones | before  | after |
| Naming | Rename "Library" to "Components" - industry-standard term | before  | after |
| Theme | Default theme matches the source site's default theme, not Claude's preference | before  | after |

  ### Usage

Works on any URL
```
/extract-design-system https://yoursite.com/
```


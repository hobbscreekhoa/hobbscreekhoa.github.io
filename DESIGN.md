# Design — The Homestead on Hobbs Creek

The site should feel like the neighborhood's entrance: a cream stone sign in front of
a line of trees under a pale sky. Every color comes from one of those three things.

## Palette

All colors live as CSS variables in `:root` at the top of `index.html`. **Add a color
there before using it anywhere else.** No brand colors (Facebook blue, Google purple,
etc.) — icons take the palette tint that matches their meaning.

### Green — the trees and the sign's lettering
| Token | Hex | Use |
|---|---|---|
| `--ink` | `#1E3A2F` | Body text, headings, sign lettering, primary button |
| `--foliage` | `#3F6B46` | Primary button hover, green icons |
| `--leaf-lt` | `#E7F0EA` | Green icon badge background |
| `--muted` | `#5A6B61` | Secondary text (a gray with green in it, never a neutral gray) |

### Creek blue — the sky and anything interactive
| Token | Hex | Use |
|---|---|---|
| `--creek` | `#2E7FA8` | Hover borders, active nav underline, focus rings |
| `--creek-dk` | `#235F7E` | Hovered link text, inline links, blue icons |
| `--creek-lt` | `#E9F3F9` | Nav bar, top of hero, footer, blue icon badges |
| `--rule-creek` | `rgba(46,127,168,.16)` | Dividers on a blue background |

### Stone — the sign itself
| Token | Hex | Use |
|---|---|---|
| `--stone` | `#C9BA96` | Sign outlines |
| `--stone-d` | `#8A7448` | Document icons, row arrows |
| `--stone-lt` | `#F5EFE1` | Document icon badges, sign caps |
| `--rule` | `#EAE2D2` | Card borders, dividers on a cream background |

### Neutrals
| Token | Hex | Use |
|---|---|---|
| `--cream` | `#FCFAF5` | Page background |
| `--card` | `#FFF` | Cards, panels, secondary buttons |

### Artwork-only colors
These are inside the SVGs (which cannot read CSS variables). Keep them in sync with
the tokens above if the palette ever changes.

- **Sign** (`index.html` hero, `logo-sign.svg`): stone gradient `#FFFFFF → #F7F2E6`,
  pillar gradient `#F2EBDC → #FFFFFF → #EDE5D2`, base `#F8F3E8`, outline `#C9BA96`,
  lettering `#1E3A2F`.
- **Favicon** (`favicon.svg`): same as the sign, but the outline is a darker stone,
  `#B9A67C`, so it still shows at 16px on a light browser tab.
- **Tree line** (`.hero-art`, `grove.svg`): back to front `#E4EDE4`, `#C3D6C6`,
  `#8CAF95`, `#4A7452` — a ramp from mist to `--foliage`.

## Rules of thumb

- **Blue means you can click it.** Hover states, focus rings and inline links go
  creek blue. Don't use blue for decoration on cream.
- **Dividers match the surface they sit on**: `--rule` (stone) on cream and white,
  `--rule-creek` on blue (nav, footer).
- **Icon badges are tinted by meaning**: stone = documents, green = your homeowner
  account and things you fill in, blue = contact and community.
- **One dark button per group.** `.btn.pri` (ink) is the main action; everything else
  is a white `.btn` with a stone border.

## Type

- Headings: Georgia serif (`--serif`) — matches the sign's lettering.
- Everything else: the system sans (`--sans`).
- Avoid leaving a single word alone on a line in hero copy; the hero paragraph uses
  `text-wrap: balance` and breaks between sentences on wide screens.

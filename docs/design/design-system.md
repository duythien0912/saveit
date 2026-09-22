# SaveIt Design System

This is the canonical visual specification for SaveIt. The selected reference is [Home reference](assets/saveit-home-reference.png); when generated pixels and this document disagree, follow this document for behavior and accessibility, then preserve the reference's visual character.

## Character

SaveIt is compact, dependable, calm, and slightly robotic. Repetition should build muscle memory: controls stay in stable positions, feedback is immediate, and the interface does not pretend to infer intent. The Mèo mascot adds warmth at two controlled moments without turning SaveIt into a game.

Use direct Vietnamese labels, flat color, crisp line icons, and generous-enough touch targets. Prefer alignment, spacing, and subtle borders over layered cards or decoration.

## Foundations

### Color tokens

| Token | Value | Use |
| --- | --- | --- |
| `canvas` | `#FBFAF7` | App background |
| `surface` | `#FFFFFF` | Tiles, sheets, dialogs |
| `ink` | `#14213D` | Primary text and icons |
| `ink-muted` | `#647089` | Secondary text |
| `border` | `#E3E6EA` | Tile and container outlines |
| `primary` | `#1267E8` | Active navigation and filled actions |
| `primary-soft` | `#DDEBFB` | Water, home, hygiene icon wells |
| `amber-soft` | `#FCE8B8` | Wake and meal icon wells |
| `coral-soft` | `#F6D7D4` | Medicine and exercise icon wells |
| `sage-soft` | `#E0EADF` | Breath, toileting, dental, relaxation icon wells |
| `violet-soft` | `#E7E0EF` | Sleep icon wells |
| `success` | `#2E8B57` | Completed confirmation when needed |
| `danger` | `#C43D3D` | Destructive confirmation only |

Colors are flat fills. Gradients, luminous glows, and decorative glass effects are outside the SaveIt language. The floating navigation may use a nearly opaque frosted surface, but active controls use one solid `primary` fill.

### Typography

Bundle Inter Variable for consistent Vietnamese rendering on both platforms.

| Role | Size / line height | Weight |
| --- | --- | --- |
| Display | 36 / 44 | 700 |
| Screen title | 28 / 36 | 700 |
| Section title | 20 / 28 | 650 |
| Action label | 15 / 20 | 600 |
| Body | 15 / 22 | 400 |
| Supporting | 13 / 18 | 400 |
| Caption | 12 / 16 | 500 |

Allow platform text scaling through 200%. At large scales, Action tiles may grow vertically and the grid may reduce from three columns to two; labels never truncate a safety-relevant Action such as Uống thuốc.

### Spacing, shape, and elevation

- Base unit: 4 dp.
- Screen gutter: 16 dp; compact gutter may be 12 dp on narrow devices.
- Grid gap: 8 dp.
- Minimum touch target: 48 by 48 dp.
- Action tile radius: 14 dp; sheets and dialogs: 20 dp; floating navigation: 28 dp.
- Borders: 1 dp `border`.
- Elevation is reserved for transient snackbar, floating navigation, sheets, and dialogs. Use one soft neutral shadow; never stack multiple shadows.

### Icons

Use one rounded line-icon family throughout, 1.75–2 dp optical stroke. Icons must convey the Action without depending on color. Do not use emoji or hand-drawn replacements for functional icons. The plus icon is always white on solid `primary`.

## Mascot system

The authoritative assets are `assets/meo_v2_alpha.png` and `assets/meo_spritesheet_v2.json`. The PNG is a transparent 1774 by 887 texture atlas; crop frames from the JSON alpha bounds. Bind the atlas to the actual repository PNG path rather than relying on the JSON `image` filename.

### Header mascot

- Render one randomly chosen frame beside the Hôm nay title.
- Keep the visible mascot approximately 52–72 dp wide and no taller than the title block.
- Choose once when the Home screen becomes active; avoid changing during rebuilds or scroll.
- Exclude poses with embedded English text (`good_day_mug`, `learn_practice_repeat`) from random selection.
- Preserve aspect ratio, transparent edges, texture, and original colors.

### Check-in mascot

- After a Check-in, choose a second random frame for the snackbar.
- Prefer positive or neutral poses such as `happy_paw`, `sleepy_heart`, `heart_rest`, `peek_up`, or `belly_up_heart`.
- The snackbar pose may differ from the header pose and is selected once per snackbar presentation.
- Mascot imagery is decorative; screen readers receive the Check-in status text, not a description of the cat.

Do not use the mascot as currency, progress, streak, coach, dialog speaker, empty-state guilt, or a substitute for a functional icon.

## Components

### Action tile

- Three-column grid at the 390 dp reference width.
- Tile is fully tappable and creates a Check-in immediately.
- Icon well is circular with the Action's chosen color; icon and label use accessible ink tones.
- Label wraps to two lines; the grid order remains stable until the person explicitly reorders it.
- Press: subtle scale to 0.98 plus haptic feedback. Release creates the Check-in once; debounce rapid duplicate pointer events without preventing deliberate repeated taps.
- Long press opens the Action menu: Edit, Reorder, Archive.

### Check-in snackbar

- Floats above navigation and never covers it.
- Shows mascot, `Đã ghi nhận {Action} · {HH:mm}`, a bell-plus affordance labeled `Nhắc tôi giờ này`, and `Hoàn tác`.
- On very narrow widths, the reminder affordance may be icon-only with a semantic label; `Hoàn tác` remains text.
- Snackbar persists long enough to act (recommended 6 seconds) and pauses its timer while a sheet is open.
- Undo removes only the Check-in just created. Reminder opens the Reminder editor prefilled from that Check-in.

### Floating navigation

- One nearly opaque white capsule for Hôm nay, Lịch sử, and Nhắc nhở.
- Active destination uses a compact solid `primary` fill with white icon and label. No gradient or glow.
- Inactive destinations use `ink` on the neutral capsule.
- The solid circular plus Action sits separately to the right, aligned with the capsule. It opens Add Action and never becomes selected.
- Preserve the last selected destination after Add Action closes.

### Sheets, dialogs, and forms

Use a bottom sheet for creation and editing on phones; use a centered width-constrained dialog on wider layouts. Primary action is solid `primary`; secondary is text or outline. Destructive actions use a separate confirmation and `danger` only at the final step.

### Empty, loading, and error states

Local reads should normally be immediate. Use skeletons only during first database migration, never for routine navigation. Empty states state the next action plainly. Errors retain entered values and offer Retry; they do not use the mascot to soften or obscure the failure.

## Responsive behavior

- Compact phone: three grid columns when labels fit; two columns under large text or very narrow widths.
- Large phone: three columns with wider gutters.
- Tablet: constrain primary content to 720 dp and use four or five columns; navigation remains centered and width-constrained.
- Respect safe areas, keyboard insets, and platform back gestures.
- iOS and Android share information architecture and tokens; system pickers, permission prompts, back behavior, and notification settings links remain platform-native.

## Motion and haptics

- Standard UI transitions: 160–220 ms; sheets: 240–300 ms.
- Use ease-out for entry and ease-in for exit.
- Successful Check-in: light haptic plus tile press; snackbar slides/fades in without bounce.
- Respect reduced-motion settings by removing scale and translating transitions in favor of opacity.
- Haptics follow the in-app setting and system capability.

## Accessibility

- Every Action tile announces `{Action}, nút ghi nhận`.
- After logging, announce `Đã ghi nhận {Action} lúc {time}` once.
- Reminder and Undo are separate accessible actions.
- Never encode Action identity or Reminder state by color alone.
- Reading and focus order follows visible order; snackbar actions are reachable without moving focus unexpectedly.
- Contrast meets WCAG AA; interactive text and icons target 4.5:1 unless large-format criteria apply.

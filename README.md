**English** | [Tiếng Việt](README.vi.md)

# Aurora Home theme for Home Assistant

A frosted-glass theme for Home Assistant: a pink, orange, blue and purple gradient background; dark, translucent, rounded cards; white text; bright, clear state colors. Devices that are on stand out with a white background, so one glance tells you which are on and which are off.

The theme only changes colors and styling. It does not change the dashboard layout, does not depend on any entity and does not load images from outside.

Requires Home Assistant 2026.8 or later.

## Screenshots

Screenshots of the **Aurora Home Plus** variant on a phone.

| Overview | Rooms | Energy |
|:---:|:---:|:---:|
| <img src="https://raw.githubusercontent.com/lipnguyen-ha/ha-aurora-home-theme/main/screenshots/01-overview.png" width="260" alt="Overview: summary bar, tiles that are on with a white background, tiles that are off with a dark background"> | <img src="https://raw.githubusercontent.com/lipnguyen-ha/ha-aurora-home-theme/main/screenshots/02-rooms.png" width="260" alt="Rooms: tiles, Bubble Card and IR remotes"> | <img src="https://raw.githubusercontent.com/lipnguyen-ha/ha-aurora-home-theme/main/screenshots/03-energy.png" width="260" alt="Energy: gauge, data tiles and chart"> |
| Tiles that are on have a white background, tiles that are off have a dark background with a colored icon | Tiles, Bubble Card and small buttons that are on | Data tiles, gauge and chart keep the dark background |

| System page | Selects and sliders |
|:---:|:---:|
| <img src="https://raw.githubusercontent.com/lipnguyen-ha/ha-aurora-home-theme/main/screenshots/04-system.png" width="260" alt="System page: entity list and update card"> | <img src="https://raw.githubusercontent.com/lipnguyen-ha/ha-aurora-home-theme/main/screenshots/05-controls.png" width="260" alt="Selects and sliders in an entities card"> |
| Entity list card | Selects and sliders |

The layout in the screenshots belongs to a personal dashboard. The theme only changes colors and styling; it does not create this layout.

## Two variants in one file

The file `aurora-home.yaml` contains two main themes: **Aurora Home** and **Aurora Home Plus**. The Plus variant also comes with four [other wallpaper variants](#wallpaper-variants). Install once and you have all of them; pick the one you want in your Profile.

### What they share

The two variants share all of the following:

- the gradient wallpaper, and the translucency and corner radius of cards;
- text color, font and primary color;
- the top bar, sidebar, dialogs and pop-ups;
- state colors;
- variables for Bubble Card and Mushroom.

### How they differ

The only difference is how devices that are **on** and **off** are displayed:

| | Aurora Home | Aurora Home Plus |
|---|---|---|
| Requires card-mod | No | **Yes** |
| Tile of a device that is on | Dark background as when off, only the icon changes color | White background, black text, white icon on a colored circle |
| Tile of a device that is off | Gray icon | Icon keeps the device color on a dark circle |
| Bubble Card sub-button that is on | Orange background, white text | White pill, black text |
| Large Bubble Card card when on | Unchanged | White background, black text, **if the dashboard uses the theme's variables** (see [below](#large-bubble-card-cards)) |
| Sensor tile | Dark background | Dark background |

### Wallpaper variants

The Plus variant comes with four other wallpaper variants. All of them are hand-drawn CSS gradients that use no images, and **all require card-mod** like the Plus variant.

| Wallpaper | Color tones | Theme name |
|---|---|---|
| Default | pink, orange, blue, purple | `Aurora Home` (no card-mod needed), `Aurora Home Plus` |
| Ocean | teal, sky blue, indigo | `Aurora Home Plus Ocean` |
| Sunset | deep pink, orange, coral, purple | `Aurora Home Plus Sunset` |
| Forest | green, olive yellow, teal green | `Aurora Home Plus Forest` |
| Midnight | indigo, purple, navy blue | `Aurora Home Plus Midnight` |

These variants differ only in the wallpaper and the background color of the settings pages, sidebar and menus. Everything else is the same as `Aurora Home Plus`. The screenshots above show the default variant.

Only `Aurora Home` can be used without card-mod installed.

### Dark smart-home variant: Aurora Home Things Dark

<img src="https://raw.githubusercontent.com/lipnguyen-ha/ha-aurora-home-theme/main/screenshots/06-things-dark.png" width="400" alt="Aurora Home Things Dark: a room with tiles and device cards">

`Aurora Home Things Dark` follows the style of a dark smart-home app. Its colors were sampled from the app's dark screenshots:

- An indigo to teal wallpaper, with a deep purple corner at the bottom left.
- Tiles of devices that are **on**: solid near-black `#17171A` background, white text, icon in the device color on a `#222225` circle.
- Tiles of devices that are **off**, and sensor tiles: 60% translucent deep navy, so the wallpaper shows through; light gray text and icon on a faint white circle.
- Sub-buttons: `#29292C` on cards that are on, faint white on cards that are off.
- Sky blue `#28B3F7` accent for switches, sliders and selected items. Settings pages, dialogs and menus are deep navy, and the sidebar is a navy gradient like the app's.
- Cards have 16px corners, and the theme always runs in dark mode, so hover colors in Settings stay navy even when the device is in light mode.

**Aurora Home Things Dark White** is the same theme, except that tiles that are on turn solid white with black text, and their icon sits on a light gray `#F1F1F5` circle.

Both **require card-mod** like the Plus variant and come in dark style only. `--device-color` and the `--card-on-*` variables for Bubble Card work the same way as in the Plus variant. Aurora Device Control Card needs v2.2.3 or later for the icon circle and buttons on cards that are on, and the gray name on cards that are off.

### Why there are two

A plain Home Assistant theme can only change global colors. It does not know which device is on, so it cannot change the background of just the tile that is on. The Plus variant uses card-mod to inject CSS based on the state of each tile.

### Which one to choose

- **card-mod is not installed, or you do not want to install anything extra:** choose **Aurora Home**.
- **You want devices that are on to really stand out with a white background:** install card-mod, then choose **Aurora Home Plus**.
- **The dashboard already colors cards when on with its own `card_mod`:** the Plus variant will override that color on tiles (changing it to a white background). If you want to keep your own colors, choose **Aurora Home**.

If you choose the Plus variant without card-mod installed, the theme still works and reports no error, but it will look exactly like the regular variant. If tiles that are on do not switch to a white background, check the [adding card-mod](#adding-card-mod-for-the-plus-variant) step again.

## Installation

1. Open `configuration.yaml` and make sure it has the following two lines. If you just added them, restart Home Assistant once.

   ```yaml
   frontend:
     themes: !include_dir_merge_named themes
   ```

2. Create a `themes` folder in the HA configuration folder if it does not exist yet (in the same place as `configuration.yaml`).
3. Download the file [themes/aurora-home.yaml](themes/aurora-home.yaml) and copy it into that `themes` folder.
4. Go to **Developer Tools → Actions** and run the action `frontend.reload_themes`.
5. Click the user name at the bottom of the sidebar to open your **Profile**, and under **Theme** choose **Aurora Home** or **Aurora Home Plus**.

The theme is selected per user and per browser. To go back, choose another theme in the same place.

### Installing via HACS (optional)

If you already have HACS, you can let HACS download and update the file instead of steps 2 and 3:

1. Open **HACS**, click the three-dot menu in the top corner, and choose **Custom repositories**.
2. Paste this repository's address, choose the type **Theme**, and click **Add**.
3. Find **Aurora Home Theme** in HACS and click **Download**.
4. Continue with steps 4 and 5 above.

### Adding card-mod for the Plus variant

1. Install [card-mod](https://github.com/thomasloven/lovelace-card-mod) via HACS.
2. Add card-mod to `extra_module_url` so that it is loaded before the dashboard, then restart HA:

   ```yaml
   frontend:
     themes: !include_dir_merge_named themes
     extra_module_url:
       - /hacsfiles/lovelace-card-mod/card-mod.js
   ```

## Plus variant details

- **Tiles of devices that can be turned on/off** (lights, switches, fans, air conditioners, media players, robot vacuums, locks…):
  - When on: white background, black text, white icon on a solid colored circle.
  - When off: dark background, icon keeps the device color on a dark circle.
- **Sensor tiles** keep the dark background and the default icon.
- **Bubble Card sub-buttons that are on** become a white pill with black text.

The icon color depends on the device type:

| Type | Color |
|---|---|
| Lights, switches, input_boolean | yellow `#FFCC33` |
| Fans, air conditioners, covers, humidifiers | sky blue `#35B8E8` |
| Media players | blue `#3E9BF0` |
| Robot vacuums | orange `#FF9F6B` |
| Locks | green `#30D158` |
| Sirens | red `#FF453A` |

The tile rules use `!important`, so they override even tiles that already color their own background with their own `card_mod`.

### Setting a custom color for one tile

Add the `--device-color` variable to that tile's `ha-card` with `card_mod`:

```yaml
type: tile
entity: switch.may_tinh
card_mod:
  prepend: true
  style: |
    ha-card { --device-color: #3E9BF0; }
```

### Large Bubble Card cards

The theme does not know whether a Bubble Card is on or off. If you want the large card to switch to a white background when on as well, the dashboard has to apply the colors itself in the card's `styles` and use the following theme variables, with fallback colors for other themes:

| Variable | Used for |
|---|---|
| `--card-on-background-color` | card background when on |
| `--card-on-border-color` | card border when on |
| `--card-on-text-color` | text and icons on a card that is on |
| `--card-on-sub-button-background-color` | sub-button background on a card that is on |
| `--card-on-icon-color` | main icon color on a card that is on |
| `--card-on-icon-background-mix` | strength of the icon circle, used in `color-mix()` (the theme sets `100%`) |
| `--card-off-icon-mix` | proportion of the device color in the icon when off, used in `color-mix()` (the theme sets `100%`) |
| `--card-off-icon-background-color` | icon circle when off |

Example:

```css
${state === 'on' ? '.bubble-container { background-color: var(--card-on-background-color, rgba(127,183,230,0.20)) !important; } .bubble-name, .bubble-state { color: var(--card-on-text-color, var(--primary-text-color)) !important; }' : ''}
```

## Customization

Edit `aurora-home.yaml` directly, then run `frontend.reload_themes` again.

| To change | Variable |
|---|---|
| Wallpaper | `aurora-home-wallpaper`. Each `radial-gradient` line is one color area. |
| Add a wallpaper variant of your own | Copy one of the blocks at the end of the file (for example `Aurora Home Plus Ocean`), then change its name and colors. |
| Card darkness | `aurora-home-surface`. The last number is the opacity, default `0.62`. |
| Translucency of Bubble Card pop-ups | `aurora-home-popup` |
| On color of each device type | the `state-*-color` variables |
| Spacing between sections | `ha-view-sections-row-gap` |

## Notes

- The wallpaper stays fixed to the screen and does not scroll with the page.
- The theme uses a single style for both light and dark mode.
- The Plus variant uses CSS `:has()` and `color-mix()`, which need a browser from 2023 or later.

## Related projects

- [Aurora Device Control Card](https://github.com/lipnguyen-ha/ha-aurora-device-control-card): a card that controls fans, speakers, infrared TVs (via ESPHome), air conditioners, robot vacuums and cameras in one consistent style.
- [WOL + Presence](https://github.com/lipnguyen-ha/ha-wol-presence): an integration that turns on a computer with Wake-on-LAN and reports whether the machine is awake or asleep; it works with Macs too.

## License

Released under the [MIT](LICENSE) license. You are free to use, modify and redistribute it.

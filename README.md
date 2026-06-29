[README.md](https://github.com/user-attachments/files/29461088/README.md)
# 🟣 Microsoft Teams Theme for Home Assistant

A clean, modern Home Assistant theme **inspired by the Microsoft Teams interface** — featuring a bold indigo/violet palette.

> ⚠️ This project is not affiliated with, endorsed by, or associated with Microsoft Corporation or Microsoft Teams in any way. All trademarks belong to their respective owners.

---

## 📸 Preview

![Dashboard Preview](preview.png)

---

## 🎨 Color Palette

The theme is built around a consistent semantic palette. Use these colors in your card-mod customizations to keep everything coherent.

| Name | Hex | Usage |
|------|-----|-------|
| `teams_violet` | `#5059C9` | Active states / ON / primary actions |
| `critical_red` | `#C4314B` | Alarms / critical alerts / danger thresholds |
| `warning_amber` | `#C98200` | Lights on / soft warnings / attention |
| `normal_white` | `#FFFFFF` | Neutral state / default card background |

---

## 📦 Installation

### Via HACS (recommended)

1. Open **HACS** in Home Assistant
2. Go to **Frontend**
3. Click the ⋮ menu → **Custom repositories**
4. Add `https://github.com/luigi-regolo/ha-microsoft-teams-theme` and select category **Theme**
5. Install **Microsoft Teams Theme**
6. Restart Home Assistant

### Manual installation

1. Copy `themes/microsoft_teams.yaml` into your `config/themes/` folder
2. In `configuration.yaml`, make sure you have:
   ```yaml
   frontend:
     themes: !include_dir_merge_named themes
   ```
3. Restart Home Assistant

---

## 🌗 Available Themes

| Theme name | Description |
|------------|-------------|
| `Microsoft Teams` | Light mode |

---

## ⚙️ Activation

**Via UI:** Profile → Theme → select *Microsoft Teams*

**Via automation / service call:**
```yaml
service: frontend.set_theme
data:
  name: Microsoft Teams
```

---

## 🃏 card-mod Integration

This theme is designed to work seamlessly with [card-mod](https://github.com/thomasloven/lovelace-card-mod), allowing you to create dynamic cards that change style based on entity state.

### Requirements

Make sure you have card-mod installed via HACS (**Frontend → card-mod**) and the following in your `configuration.yaml`:

```yaml
frontend:
  themes: !include_dir_merge_named themes
  extra_module_url:
    - /hacsfiles/lovelace-card-mod/card-mod.js
```

---

### Example — Dynamic Alert Card (Tile)

This example shows a **battery alert card** that turns red when battery level drops below 20%, and stays neutral otherwise.

```yaml
type: tile
entity: sensor.batterie_dispositivi
icon: mdi:battery-alert
hide_state: false
vertical: false
color: >
  {% set b = states('sensor.batterie_dispositivi') | int(100) %}
  {% if b <= 20 %}
    white
  {% else %}
    #6B6A69
  {% endif %}
card_mod:
  style: |
    ha-card {
      border-radius: 16px !important;
      overflow: hidden !important;
      {% set b = states('sensor.batterie_dispositivi') | int(100) %}
      {% if b <= 20 %}
        background: #C4314B !important;
        border: 1px solid rgba(196, 49, 75, 0.65) !important;
        box-shadow: 0 4px 12px rgba(196, 49, 75, 0.30) !important;
        --primary-text-color: #FFFFFF !important;
        --secondary-text-color: rgba(255, 255, 255, 0.92) !important;
        --tile-color: #FFFFFF !important;
      {% else %}
        background: #FFFFFF !important;
        border: 1px solid rgba(107, 106, 105, 0.18) !important;
        box-shadow: 0 1px 3px rgba(0,0,0,0.08) !important;
        --primary-text-color: #242424 !important;
        --secondary-text-color: #6B6A69 !important;
        --tile-color: #6B6A69 !important;
      {% endif %}
    }
    ha-state-icon {
      {% set b = states('sensor.batterie_dispositivi') | int(100) %}
      {% if b <= 20 %}
        color: #FFFFFF !important;
      {% else %}
        color: #6B6A69 !important;
      {% endif %}
    }
```

**How it works:**
- 🔴 Battery ≤ 20% → card turns `critical_red` (`#C4314B`) with white text and icon
- ⚪ Battery > 20% → card stays neutral white with grey text

You can adapt this pattern to any sensor by replacing `sensor.batterie_dispositivi` with your entity and adjusting the threshold and colors from the palette above.

---

## 📄 License

MIT License — free to use, modify and share.

---

*This theme is inspired by the Microsoft Teams UI. Not affiliated with Microsoft Corporation.*

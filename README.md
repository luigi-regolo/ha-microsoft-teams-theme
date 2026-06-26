# 🟣 Microsoft Teams Theme for Home Assistant

A clean, modern Home Assistant theme inspired by the **Microsoft Teams** interface — featuring the iconic Teams Purple palette with full support for both light and dark mode.

---

## 🎨 Color Palette

| Role | Color | Hex |
|------|-------|-----|
| Primary / Accent | Teams Purple | `#6264A7` |
| Sidebar Dark | Charcoal | `#292929` |
| Header Dark | Teams Violet | `#464775` |
| Background Light | Off-White | `#F5F5F5` |
| Background Dark | Near Black | `#201F1E` |
| Error | Teams Red | `#C4314B` |
| Success | Teams Green | `#237B4B` |

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
| `microsoft_teams` | Light mode with auto dark variant |
| `microsoft_teams_dark` | Dedicated dark mode |

---

## ⚙️ Activation

**Via UI:** Profile → Theme → select *Microsoft Teams* or *Microsoft Teams Dark*

**Via automation / service call:**
```yaml
service: frontend.set_theme
data:
  name: microsoft_teams
```

---

## 📄 License

MIT License — free to use, modify and share.

---

*Made with 💜 for the Home Assistant community*

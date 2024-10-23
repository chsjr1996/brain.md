#gnome #produtividade

## Lista de extensões utilizadas:
- AATWS (Seletor de janelas + lançador de aplicativos)
- Blur my Shell (Transparência + blur)
- Dash to Dock (Dock fixo)
- Just Perfection (Alterações visuais no Gnome Shell)
- Night Theme Switcher (Gerenciador de tema diurno/noturno)
- Pano - Clipboard Manager (Gerenciador da área de transferência)
- Vitals (Monitoramento de hardware)
- Weather O'Clock (Indicador do clima)

## Configurações e ajustes
### AATWS
- **Placement:** Bottom
- **Tooltip Titles:** Disable

### Blur my Shell
- **Panel blur:** Inactive
- **Background blur - Overview components style:** Dark

### Just Perfection
- **Visibility - Weather:** Inactive
- **Visibility - Window Picker Caption:** Inactive
- **Customize - Workspace Switcher Size:** 10%

### Night Theme Switcher
- **Manual schedule:** Active
	- **Sunrise:** 06:00 AM
	- **Sunset:** 05:30 PM
- **Keyboard shortcut:** Super+T
- **Run commands:** Active
	- **Sunrise:** `gsettings set org.gnome.desktop.interface gtk-theme "Adwaita"`
	- **Sunset:** `gsettings set org.gnome.desktop.interface gtk-theme "Adwaita-dark"`

### Pano - Clipboard Manager
- **History Length:** 100
- **Global Shortcut:** Super+V
- **Incognito Mode Shortcut:** Shift+Super+V
- **Opções desativadas:**
	- Sync Primary
	- Paste on Select
	- Send Notification on Copy
	- Play an Audio on Copy
	- Keep Search Entry
	- Show Indicator
	- Wiggle Indicator
	- Link Previews
	- Open Links in Browser

### Vitals
- **General - Menu always centered:** Active
- **Indicadores usados:**
	- Memory > Usage
	- Processor > Usage
	- Temperature > k10temp Tctl
	- Storage > Free

### Weather O'Clock
Ajuste realizado no 'schema' do Gnome para mudar unidade para "Celsius". [[Gnome - Usar localização não registrada no GWeather|Veja mais]].
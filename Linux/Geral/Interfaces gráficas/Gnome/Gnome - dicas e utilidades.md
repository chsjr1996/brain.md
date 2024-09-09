#gnome

## Remover ícone da aplicação na barra de título
Para remover o ícone da barra de título no terminal execute:

```
gsettings set org.gnome.desktop.wm.preferences button-layout appmenu:close
```
> Ou pelo dconf-editor definir o valor padrão.

## Usar localização não registrada no GWeather
Algumas localizações não estão disponível no Gnome Weather, porém é possível adicionar através do script abaixo:

![[gnome_weather.sh]]
> [!example] Referências
> - https://discourse.gnome.org/t/how-to-add-my-location-for-the-weather/18478
> - https://gitlab.com/julianfairfax/scripts/-/blob/main/add-location-to-gnome-weather.sh

## Mudança na unidade de temperatura para 'Celsius'
Usar o "dconf-editor" para mudar a unidade no seguinte caminho:

```
/org/gnome/GWeather4/temperature-unit
```

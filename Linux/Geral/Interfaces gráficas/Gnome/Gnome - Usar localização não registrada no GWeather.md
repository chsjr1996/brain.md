Algumas localizações não estão disponível no Gnome Weather, porém é possível adicionar através do script abaixo:

![[gnome_weather.sh]]
> [!example] Referências
> - https://discourse.gnome.org/t/how-to-add-my-location-for-the-weather/18478
> - https://gitlab.com/julianfairfax/scripts/-/blob/main/add-location-to-gnome-weather.sh

> [!NOTE] Mudar unidade da temperatura
> Usar o "dconf-editor" para mudar a unidade no seguinte caminho:
> ```
> /org/gnome/GWeather4/temperature-unit
> ```
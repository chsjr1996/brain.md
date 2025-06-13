Algumas localizações não estão disponível no Gnome Weather, porém é possível adicionar através do script abaixo:

![[gnome_weather.sh]]
> [!example] Referências
> - https://discourse.gnome.org/t/how-to-add-my-location-for-the-weather/18478
> - https://gitlab.com/julianfairfax/scripts/-/blob/main/add-location-to-gnome-weather.sh

Exemplo de escrita nos registros do dconf:
```ini
[<(uint32 2, <('Delfim Moreira', '', false, [(-0.39285054665849561, -0.79027181741324681)], @a(dd) [])>)>]
```

---

> [!NOTE] Mudar unidade da temperatura
> Usar o "dconf-editor" para mudar a unidade no seguinte caminho:
> ```
> /org/gnome/GWeather4/temperature-unit
> ```
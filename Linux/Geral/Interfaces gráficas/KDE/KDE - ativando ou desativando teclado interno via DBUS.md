É possível ativar/desativar dispositivos controlados pelo compositor KWin através do DBUS. O script abaixo permite realizar este procedimento de forma simples, bastando especificar uma lista com a identificação dos dispositivos que deverão ser afetados.

```sh
#!/usr/bin/env bash

SERVICE="org.kde.KWin"
DBUS_PATH="/org/kde/KWin/InputDevice"
INTERFACE="org.kde.KWin.InputDevice"
METHOD_GET="org.freedesktop.DBus.Properties.Get"
METHOD_SET="org.freedesktop.DBus.Properties.Set"

declare -A devices=(
    ["AT Translated Set 2 keyboard"]=''
)

find_devices() {
    local DM_INTERFACE="org.kde.KWin.InputDeviceManager"
    local DM_PROPERTY="devicesSysNames"

    for sysname in $(qdbus-qt6 "$SERVICE" "$DBUS_PATH" "$METHOD_GET" "$DM_INTERFACE" "$DM_PROPERTY"); do
        name=$(qdbus-qt6 "$SERVICE" "${DBUS_PATH}/${sysname}" "$METHOD_GET" "$INTERFACE" name)

        for device in "${!devices[@]}"; do
            if [ "$name" == "$device" ]; then
                devices["$device"]="$sysname"
            fi
        done
    done
}

check_devices() {
    local return_code=0
    for device in "${!devices[@]}"; do
        sysname=${devices["$device"]}
        if [ -z "$device" ]; then
            echo "Failed to find device ($device)"
            return_code=1
        fi
    done
    return "$return_code"
}

get_device_status() {
    qdbus-qt6 "$SERVICE" "${DBUS_PATH}/$1" "$METHOD_GET" "$INTERFACE" "enabled"
}

set_device_status() {
    qdbus-qt6 "$SERVICE" "${DBUS_PATH}/$1" "$METHOD_SET" "$INTERFACE" "enabled" "$2"
}

toggle_device() {
    status=$(get_device_status "$1")
    status=$([[ "$status" == "false" ]] && echo true || echo false)
    set_device_status "$1" "$status"
}

find_devices
if ! check_devices; then
    exit 1
fi

for device in "${!devices[@]}"; do
    sysname=${devices["$device"]}
    case "$1" in
        "enable") set_device_status "$sysname" true ;;
        "disable") set_device_status "$sysname" false ;;
        "toggle") toggle_device "$sysname" ;;
        "status") echo "$device: $(get_device_status "$sysname" )"
    esac
done
```

# Referência
- [Sporif/kwin-input-devices](https://gist.github.com/Sporif/0e52e4b0eaf071cfbf19f3381ba3d65a)
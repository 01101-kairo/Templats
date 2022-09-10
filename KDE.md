```
Lista de exemplos de comandos do KDE Connect
No KDE Connect, você pode adicionar seus próprios comandos e executá-los a
partir do seu telefone. Aqui estão alguns comandos úteis. Sinta-se livre para adicionar o seu próprio!Controle o estado do seu computador
Desligar:
systemctl poweroff
Reiniciarː
systemctl reboot
Suspender:
systemctl suspend
Hibernar:
systemctl hibernate
Bloquear a tela:
loginctl lock-session
Desbloquear a tela:
loginctl unlock-session
Desligar a tela:
xset dpms force off
Ligar a Tela:
xset dpms force on
Travar o teclado e o mouse (não a tela):
pyxtrlock
Desbloquear o teclado e o mouse:
pkill pyxtrlock
Controle o volume
Plasma
Abaixar o volume:
qdbus org.kde.kglobalaccel /component/kmix invokeShortcut "decrease_volume"
Aumentar o volume:
qdbus org.kde.kglobalaccel /component/kmix invokeShortcut "increase_volume"
Silenciar:
qdbus org.kde.kglobalaccel /component/kmix invokeShortcut "mute"
Silenciar o microfone:
qdbus org.kde.kglobalaccel /component/kmix invokeShortcut "mic_mute"
Outros DE/WM (com pactl)
Abaixar volume:
pactl set-sink-volume $(pactl list short sinks | grep RUNNING | cut -f1) -10%
Aumentar volume:
pactl set-sink-volume $(pactl list short sinks | grep RUNNING | cut -f1) +10%
Mutar/Desmutar:
pactl set-sink-mute $(pactl list short sinks | grep RUNNING | cut -f1) toggle
Outros DE/WM (com amixer)
Abaixar volume:
amixer -q sset Master 10%-
Aumentar volume:
amixer -q sset Master 10%+
Outros comandos podem ser criados usando amixer
Mudar a aparência
Tema Breeze (Claro)
lookandfeeltool -a 'org.kde.breeze.desktop'
Tema Breeze (Escuro) theme:
lookandfeeltool -a 'org.kde.breezedark.desktop'
Configurações de brilho
Aumentar Brilho:
qdbus org.kde.Solid.PowerManagement /org/kde/Solid/PowerManagement/Actions/BrightnessControl org.kde.Solid.PowerManagement.Actions.BrightnessControl.setBrightness $(expr $(qdbus org.kde.Solid.PowerManagement /org/kde/Solid/PowerManagement/Actions/BrightnessControl org.kde.Solid.PowerManagement.Actions.BrightnessControl.brightness) + 375)
Diminuir Brilho:
qdbus org.kde.Solid.PowerManagement /org/kde/Solid/PowerManagement/Actions/BrightnessControl org.kde.Solid.PowerManagement.Actions.BrightnessControl.setBrightness $(expr $(qdbus org.kde.Solid.PowerManagement /org/kde/Solid/PowerManagement/Actions/BrightnessControl org.kde.Solid.PowerManagement.Actions.BrightnessControl.brightness) - 375)
Captura de Tela
Salvar Localmente:
spectacle -b
Enviar para o smartphone:
file=/tmp/$(hostname)_$(date "+%Y%m%d_%H%M%S").png; spectacle -bo "${file}" && kdeconnect-cli -d $(kdeconnect-cli -a --id-only) --share ${file}

```

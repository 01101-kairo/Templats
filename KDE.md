<p>
<br />Lista de exemplos de comandos do KDE Connect
<br />No KDE Connect, você pode adicionar seus próprios comandos e executá-los a
<br />partir do seu telefone. Aqui estão alguns comandos úteis. Sinta-se livre para adicionar o seu próprio!Controle o estado do seu computador
<br />Desligar:
<br />systemctl poweroff
<br />Reiniciarː
<br />systemctl reboot
<br />Suspender:
<br />systemctl suspend
<br />Hibernar:
<br />systemctl hibernate
<br />Bloquear a tela:
<br />loginctl lock-session
<br />Desbloquear a tela:
<br />loginctl unlock-session
<br />Desligar a tela:
<br />xset dpms force off
<br />Ligar a Tela:
<br />xset dpms force on
<br />Travar o teclado e o mouse (não a tela):
<br />pyxtrlock
<br />Desbloquear o teclado e o mouse:
<br />pkill pyxtrlock
<br />Controle o volume
<br />Plasma
<br />Abaixar o volume:
<br />qdbus org.kde.kglobalaccel /component/kmix invokeShortcut "decrease_volume"
<br />Aumentar o volume:
<br />qdbus org.kde.kglobalaccel /component/kmix invokeShortcut "increase_volume"
<br />Silenciar:
<br />qdbus org.kde.kglobalaccel /component/kmix invokeShortcut "mute"
<br />Silenciar o microfone:
<br />qdbus org.kde.kglobalaccel /component/kmix invokeShortcut "mic_mute"
<br />Outros DE/WM (com pactl)
<br />Abaixar volume:
<br />pactl set-sink-volume $(pactl list short sinks | grep RUNNING | cut -f1) -10%
<br />Aumentar volume:
<br />pactl set-sink-volume $(pactl list short sinks | grep RUNNING | cut -f1) +10%
<br />Mutar/Desmutar:
<br />pactl set-sink-mute $(pactl list short sinks | grep RUNNING | cut -f1) toggle
<br />Outros DE/WM (com amixer)
<br />Abaixar volume:
<br />amixer -q sset Master 10%-
<br />Aumentar volume:
<br />amixer -q sset Master 10%+
<br />Outros comandos podem ser criados usando amixer
<br />Mudar a aparência
<br />Tema Breeze (Claro)
<br />lookandfeeltool -a 'org.kde.breeze.desktop'
<br />Tema Breeze (Escuro) theme:
<br />lookandfeeltool -a 'org.kde.breezedark.desktop'
<br />Configurações de brilho
<br />Aumentar Brilho:
<br />qdbus org.kde.Solid.PowerManagement /org/kde/Solid/PowerManagement/Actions/BrightnessControl org.kde.Solid.PowerManagement.Actions.BrightnessControl.setBrightness $(expr $(qdbus org.kde.Solid.PowerManagement /org/kde/Solid/PowerManagement/Actions/BrightnessControl org.kde.Solid.PowerManagement.Actions.BrightnessControl.brightness) + 375)
<br />Diminuir Brilho:
<br />qdbus org.kde.Solid.PowerManagement /org/kde/Solid/PowerManagement/Actions/BrightnessControl org.kde.Solid.PowerManagement.Actions.BrightnessControl.setBrightness $(expr $(qdbus org.kde.Solid.PowerManagement /org/kde/Solid/PowerManagement/Actions/BrightnessControl org.kde.Solid.PowerManagement.Actions.BrightnessControl.brightness) - 375)
<br />Captura de Tela
<br />Salvar Localmente:
<br />spectacle -b
<br />Enviar para o smartphone:
<br />file=/tmp/$(hostname)_$(date "+%Y%m%d_%H%M%S").png; spectacle -bo "${file}" && kdeconnect-cli -d $(kdeconnect-cli -a --id-only) --share ${file}
</p>
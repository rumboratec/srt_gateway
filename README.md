# srt_gateway

srt-live-transmit "udp://192.168.15.176:5001?rcvbuf=1000000" "srt://:1057?mode=listener&latency=1000&linger=0&tsbpd=1&tlpktdrop=1&conntimeout=3000"


MEDIATX
MISTSERVER
opensrthub

pkill ffmpeg matar todos processos

srt-live-transmit "udp://192.168.15.176:5002?rcvbuf=10000000" "srt://:1057?mode=listener&latency=1000&linger=0&conntimeout=500&driftconf=10&kmrefreshrate=1024"

Aqui o comando cria um "servidor" SRT esperando alguém se conectar.

mode=listener: Significa que o seu computador fica parado, ouvindo a porta 1057, esperando o "cliente" (VLC) ligar para ele.

latency=1000: Define um atraso proposital de 1 segundo. O SRT usa esse tempo para pedir de volta pacotes que se perderam no caminho. Se um pacote some, o sistema tem 1 segundo para recuperá-lo antes que o vídeo trave.

linger=0: Comando de "desconexão imediata". Quando o cliente (VLC) fecha, o SRT encerra a sessão na hora, sem tentar manter a conexão aberta por segurança. Isso ajuda na reconexão rápida.

3. Parâmetros de Estabilidade e Segurança
conntimeout=500: Se a conexão falhar, o SRT desiste de tentar em 0,5 segundos. Isso evita que o processo fique "preso" em uma conexão fantasma (zumbi) e permite que você reinicie o player rapidamente.

driftconf=10: Gerencia a correção de relógio (clock). Ele ajusta a velocidade com que os pacotes são liberados para evitar que o áudio e o vídeo percam o sincronismo ao longo do tempo.

kmrefreshrate=1024: Relacionado à criptografia (Key Management). Ele define a frequência com que as chaves de segurança são atualizadas. Como você não definiu uma senha (passphrase), ele tem pouco efeito prático, mas ajuda a manter a estrutura do protocolo padrão.


srt://177.19.248.199:1057?mode=caller&latency=1000&conntimeout=500
srt-live-transmit -s 1000 "udp://192.168.15.176:5003" "srt://192.168.192.86:1057?mode=listener&latency=3000"


# Laborator 2

## Cuprins
- [Introducere si IDE](https://github.com/senisioi/computer-networks/blob/master/laborator2/README.md#intro)
- [python 2.7 basics](https://github.com/senisioi/computer-networks/blob/master/laborator2/README.md#basics)
- [Exercitii python](https://github.com/senisioi/computer-networks/blob/master/laborator2/README.md#exercitii_python)
- [Socket API](https://github.com/senisioi/computer-networks/blob/master/laborator2/README.md#socket)
- [UDP](https://github.com/senisioi/computer-networks/blob/master/laborator2/README.md#udp)
- [Exercitii socket UDP](https://github.com/senisioi/computer-networks/blob/master/laborator2/README.md#exercitii_udp)
- [TCP](https://github.com/senisioi/computer-networks/blob/master/laborator2/README.md#tcp)
- [Exercitii socket TCP](https://github.com/senisioi/computer-networks/blob/master/laborator2/README.md#exercitii_tcp)


<a name="intro"></a> 
## Introducere
In cadrul acestui capitol vom lucra cu [python](http://www.bestprogramminglanguagefor.me/why-learn-python), un limbaj de programare foarte simplu pe care il vom folosi pentru a crea si trimite pachete pe retea.

Pentru debug si autocomplete, este bine sa avem un editor si [IDE pentru acest limbaj](https://wiki.python.org/moin/IntegratedDevelopmentEnvironments). In cadrul orelor vom lucra cu [wingide](http://wingware.com/downloads/wing-personal), dar pe calculatoarele voastre personale puteti lucra cu orice alt editor. 
Pentru a instala wingide fara permisiuni de administrator, putem rula:
```bash
wget https://gist.githubusercontent.com/senisioi/7d3d8a223f23d8bc9a21464dbe5f7e47/raw/e6657e66c441e2554fb8d3777783ca0eb6a2c985/install-wing.sh
bash install-wing.sh
```
[Scriptul](https://gist.github.com/senisioi/772b4b87b4fb52b96e6b83a22a4299b5) va instala editorul in directorul $HOME. 
Pentru a lansa wingide, putem sa rulam in terminal:
```bash
wing-personal
```
Daca aplicatia nu exista, puteti sa o adaugati in path sau puteti incerca sa o instalati din nou.

Pentru a face editorul sa arate mai bine, rulati din linia de comanda:
```bash
cat <<EOF >> ~/.wingpersonal6/preferences
[user-preferences]
edit.show-line-numbers = 1
gui.qt-color-palette = u'one-dark'
gui.use-palette-throughout-ui = True
EOF
```

<a name="basics"></a> 
## [python 2.7 basics](https://www.tutorialspoint.com/python/python_variable_types.htm)
```python
# comment pentru hello world
variabila = 'hello "world"'
print variabila

# int:
x = 1 + 1

# str:
xs = str(x) + ' ' + variabila

# tuplu
tup = (x, xs)

# lista
l = [1, 2, 2, 3, 3, 4, x, xs, tup]
print l[2:]

# set
s = set(l)
print s
print s.intersection(set([4, 4, 4, 1]))

# dict:
d = {'grupa': 123, "nr_studenti": 10}
print d['grupa'], d['nr_studenti']
```

#### [for](https://www.tutorialspoint.com/python/python_for_loop.htm) si [while](https://www.tutorialspoint.com/python/python_while_loop.htm)
```python
lista = [1,5,7,8,2,5,2]
for element in lista:
    print element

for idx, element in enumerate(lista):
    print idx, element

for idx in range(0, len(lista)):
    print lista[idx]

idx = 0
while idx < len(lista):
    print lista[idx]
    idx += 1 
```

#### [if else](https://www.tutorialspoint.com/python/python_if_else.htm)
```python
'''
   comment pe
   mai multe
   linii
'''
x = 1
y = 2
print x + y
if (x == 1 and y == 2) or (x==2 and y == 1):
    print " x e egal cu:", x, ' si y e egal cu: ', y
elif x == y:
    print 'sunt la fel'
else:
    print "nimic nu e adevarat"
```

#### [functii](https://www.tutorialspoint.com/python/python_functions.htm)
```python
def functie(param = 'oooo'):
    '''dockblock sunt comments in care explicam
    la ce e buna functia
    '''
    return "whooh " + param + "!"

def verifica(a, b):
    ''' aceasta functie verifica
    o ipoteza interesanta
    '''
    if (x == 1 and y == 2) or (x==2 and y == 1):
        return 1
    elif x == y:
        return 0
    return -1
```

#### [module](https://www.tutorialspoint.com/python/python_modules.htm)
```python
import os
import sys
import logging
from os.path import exists
import time

logging.basicConfig(format = u'[LINE:%(lineno)d]# %(levelname)-8s [%(asctime)s]  %(message)s', level = logging.NOTSET)
logging.info("Mesaj de informare")
logging.warn("Mesaj de warning")
logging.error("Mesaj de eroare")
try:
    1/0
except:
    logging.exception("Un mesaj de exceptie!")

program_name = sys.argv[0]
print program_name
print "Exista '/elocal'?", exists('/elocal')
print os.path.join('usr', 'local', 'bin')

for element in "hello world":
    sys.stdout.write(element)
    sys.stdout.flush()
    time.sleep(1)
```

#### [main](https://stackoverflow.com/questions/4041238/why-use-def-main)
```python
def main():
    print "functia main"

# un if care verifica daca scriptul este importat sau apelat ca main
if __name__ == '__main__':
    main()
 ```

#### [clase](https://www.tutorialspoint.com/python/python_classes_objects.htm)
```python
class Grupa:
    nume = 'grp'
    def __init__(self, nume, numar_studenti):
        self.nume = nume
        self.numar_student = numar_studenti
    def _metoda_protected(self):
        print "da"
    def __metoda_privata(self):
        print 'nu'
    def metoda_publica(self):
        print "yes"


g = Grupa('222', '21')
print g.nume
print g.numar_studenti
print G.nume
```

<a name="exercitii_python"></a> 
### Exercitii
1. Creati un script de python care printeaza toate literele unui text, cate o litera pe secunda, folosind `time.sleep(1)`.
2. Rulati scriptul anterior intr-un container.
3. Folosind [command](https://docs.docker.com/compose/compose-file/compose-file-v2/#command), modificati docker-compose.yml pentru a lansa acel script ca proces al containerului.

<a name="socket"></a> 
## Socket API
Este un [API](https://www.youtube.com/watch?v=s7wmiS2mSXY) disponibil in mai toate limbajele de programare cu care putem implementa comunicarea pe retea la un nivel mai inalt. Semnificatia flag-urilor este cel mai bine explicata in tutoriale de [unix sockets](https://www.tutorialspoint.com/unix_sockets/socket_core_functions.htm) care acopera partea de C. In limbajul [python](https://docs.python.org/2/library/socket.html) avem la dispozitie exact aceleasi functii si flag-uri ca in C iar interpretarea lor nu tine de un limbaj de programare particular.

<a name="udp"></a> 
### User Datagram Protocol - [UDP](https://tools.ietf.org/html/rfc768)

Este un protocol simplu la [nivelul transport](https://www.youtube.com/watch?v=hi9BVTNvl4c&list=PLfgkuLYEOvGMWvHRgFAcjN_p3Nzbs1t1C&index=50). Header-ul acestuia include portul sursa, portul destinatie, lungime si un checksum optional:
```
  0      7 8     15 16    23 24    31
  +--------+--------+--------+--------+
  |     Source      |   Destination   |
  |      Port       |      Port       |
  +--------+--------+--------+--------+
  |                 |                 |
  |     Length      |    Checksum     |
  +--------+--------+--------+--------+
  |
  |          data octets ...
  +---------------- ...
```
Cateva caracteristi ale protocolului sunt descrise [aici](https://en.wikipedia.org/wiki/User_Datagram_Protocol#Attributes) iar partea de curs este acoperita in mare parte [aici](https://www.youtube.com/watch?v=Z1HggQJG0Fc&index=51&list=PLfgkuLYEOvGMWvHRgFAcjN_p3Nzbs1t1C).

Server-ul se instantiaza cu [AF_INET](https://stackoverflow.com/questions/1593946/what-is-af-inet-and-why-do-i-need-it) si SOCK_DGRAM (datagrams - connectionless, unreliable messages of a fixed maximum length) pentru UDP:
```python
# UDP socket 
sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

port = 10000
adresa = 'localhost'
server_address = (adresa, port)
sock.bind(server_address)

data, address = sock.recvfrom(4096)

print data, address

sent = sock.sendto(data, address)

sock.close()
```

Clientul trebuie sa stie la ce adresa ip si pe ce port sa comunice cu serverul:
```python
sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

port = 10000
adresa = 'localhost'
server_address = (adresa, port)

sent = sock.sendto(mesaj, server_address)
data, server = sock.recvfrom(4096)

sock.close()
```

O diagrama a procesului anterior este reprezentata aici:
![alt text](https://raw.githubusercontent.com/senisioi/computer-networks/master/laborator2/UDPsockets.jpg)


<a name="exercitii_udp"></a> 
### Exercitii
1. Pe container-ul rt1 rulati [udp_server.py](https://github.com/senisioi/computer-networks/blob/master/laborator2/src/udp_server.py), [udp_client.py](https://github.com/senisioi/computer-networks/blob/master/laborator2/src/udp_client.py). 
2. Incercati sa folositi udp_client.py pentru a va conecta de pe sistemul host la container-ul rt1. Verificati documentatia de la [ports](https://docs.docker.com/compose/compose-file/compose-file-v2/#ports)
3. Care este portul destinatie pe care il foloseste server-ul pentru a trimite un mesaj clientului?
4. Modificati mesajul client-ului ca acesta sa fie citit ca parametru al scriptului (`sys.argv[1]`). Transmiteti mesaje de la un container la altul folosind *udp_server.py* si *udp_client.py*.
5. Utilizati `tcpdump -nvvX -i any udp port 10000` pentru a scana mesajele UDP care circula pe portul 10000.


<a name="tcp"></a> 
### Trasnmission Control Protocol - [TCP](https://tools.ietf.org/html/rfc793#page-15)

Este un protocol mai avansat de la [nivelul transport](http://www.erg.abdn.ac.uk/users/gorry/course/inet-pages/transport.html). 
Header-ul acestuia este mai complex:
```
  0                   1                   2                   3   Offs.
  0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 
 -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
 |          Source Port          |       Destination Port        |  1
 -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
 |                        Sequence Number                        |  2
 -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
 |                    Acknowledgment Number                      |  3
 -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
 | Data  |0 0 0| |C|E|U|A|P|R|S|F|                               |
 |Offset | Res.|N|W|C|R|C|S|S|Y|I|            Window             |  4
 |       |     |S|R|E|G|K|H|T|N|N|                               |
 -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
 |           Checksum            |         Urgent Pointer        |  5
 -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
 |                    Options   (if data offset > 5)             | 
 -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
 |                    Application data                           | 
 -+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-
```


Cateva caracteristi ale protocolului sunt descrise [aici](https://en.wikipedia.org/wiki/Transmission_Control_Protocol#TCP_segment_structure) iar partea de curs este acoperita in mare parte [aici](https://www.youtube.com/watch?v=c6gHTlzy-7Y&list=PLfgkuLYEOvGMWvHRgFAcjN_p3Nzbs1t1C&index=52).

Server-ul se instantiaza cu [AF_INET](https://stackoverflow.com/questions/1593946/what-is-af-inet-and-why-do-i-need-it) si SOCK_STREAM (fiindca TCP opereaza la nivel de [byte streams](https://softwareengineering.stackexchange.com/questions/216597/what-is-a-byte-stream-actually))

```python
# TCP socket 
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

port = 10000
adresa = 'localhost'
server_address = (adresa, port)
sock.bind(server_address)

sock.listen(5)
while True:
   conexiune, addr = sock.accept()
   time.sleep(30)
   #conexiune.send("Hello from TCP!")
   conexiune.close()

sock.close()
```

Clientul trebuie sa stie la ce adresa ip si pe ce port sa comunice cu serverul:
```python
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

port = 10000
adresa = 'localhost'
server_address = (adresa, port)

sock.connect(server_address)
#data = sock.recv(1024)

sock.close()
```

O diagrama a procesului anterior este reprezentata aici:
![alt text](https://raw.githubusercontent.com/senisioi/computer-networks/master/laborator2/TCPsockets.png)


<a name="exercitii_tcp"></a> 
### Exercitii
1. In containerul rt1 rulati `tcpdump -Snnt tcp` si tot in rt1 rulati un server tcp. Din container-ul rt2, creati o conexiune. Urmariti [three-way handshake](https://www.geeksforgeeks.org/computer-network-tcp-3-way-handshake-process/) si inchiderea conexiunii la nivel de pachete.
2. Pentru a observa retransmisiile, putem introduce un delay artificial sau putem ignora anumite pachete pe retea. Pentru asta, folosim un tool linux numit [netem](https://wiki.linuxfoundation.org/networking/netem) sau mai pe scurt [aici](https://stackoverflow.com/questions/614795/simulate-delayed-and-dropped-packets-on-linux). Aplicati o regula de ignorare a 1% din pachetele care circula pe eth0 folosind: `tc qdisc add dev eth0 root netem loss 0.1%`. Rulati comanda `tc -s qdisc` pentru a vedea filtrul adaugat pe eth0. Puteti modifica filtrul prin `tc qdisc change dev eth0 root netem loss 75%` sau puteti sa stergeti regulile folosind: `tc qdisc del dev eth0 root netem`. Puteti rula *netem* pornind un nou bash shell cu user root pe rt1, pastrati deschise tcpdump si server-ul. Conectati client-ul si observati pachetele care circula pe eth0.

<a name="shake"></a> 
### 3-way handshake
```
tcpdump -Snn tcp

SYN:
   IP 172.111.0.14.59004 > 198.13.0.14.10000: Flags [S], seq 2416620956, win 29200, options [mss 1460,sackOK,TS val 897614012 ecr 0,nop,wscale 7], length 0

SYN-ACK:
   IP 198.13.0.14.10000 > 172.111.0.14.59004: Flags [S.], seq 409643424, ack 2416620957, win 28960, options [mss 1460,sackOK,TS val 2714984427 ecr 897614012,nop,wscale 7], length 0

ACK:
   IP 172.111.0.14.59004 > 198.13.0.14.10000: Flags [.], ack 409643425, win 229, length 0

Trimite un octet cu PSH si intervalul de secventa de dimensiune 1:
   IP 172.111.0.14.59004 > 198.13.0.14.10000: Flags [P.], seq 2416620957:2416620958, ack 409643425, win 229, length 1

ACK cu sequence capatul intervalului care semnifica: am primit octeti pana la 2416620957, astept de la 2416620958 inainte:
    IP 198.13.0.14.10000 > 172.111.0.14.59004: Flags [.], ack 2416620958, win 227, length 0
```

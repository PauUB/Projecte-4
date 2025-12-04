# T05: Accés Remot. Connexió via SSH 

## Configuració de ssh

- Primer de tot instal·lem SSH
```bash
sudo apt install ssh -y
```
- Un cop instal·lat a l'arxiu `/etc/ssh/sshd_config` afegim una nova línia per poder indicar quins usuaris poden accedir al ssh.
  Indicarem que només *usuari* pot accedir
  ![allowusers](img/img06.png)
  Creem un usuari secundari anomenat *usuari2* i afegim un password a *root*
  ![ceració usuari](img/img05.png)
  ![Password root](img/img17.png)
  ![login root](img/img16.png)

- Comprovem que es pot connectar remotament a *usuari* però no a *usuari2*
  ![usuari](img/img02.png)
  ![usuari](img/img03.png)
  ![usuari](img/img07.png)

- Configurem amb redirecció dinàmica al client per redirigir el trànsit.
  ![tunel](img/img08.png)

- Configurem el proxy al client i amb WireShark capturem paquets per comprovar la connexió Client-Servidor
  ![configuració proxy](img/img09.png)
  ![Captura paquets](img/img10.png)

- Generem una clau pública
  ![Creació clau](img/img11.png)
  ![Creació clau](img/img12.png)
  ![Creació clau](img/img13.png)

- Comprovem que ens demana la clau pública per accedir
  ![Comprovació](img/img14.png)

- Instal·lem Servidor OpenSSH a Windows11
  ![server ssh](img/img15.png)

- Iniciem el servei i indiquem que inici automaticament
![inicia servei](img/img18.png)
![indicacio inici](img/img19.png)

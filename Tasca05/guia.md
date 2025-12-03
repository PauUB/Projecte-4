# T05: Accés Remot. Connexió via SSH 

## Configuració de ssh

- Primer de tot instal·lem SSH
```bash
sudo apt install ssh -y
```
- Un cop instal·lat a l'arxiu `/etc/ssh/sshd_config` afegim una nova línia per poder indicar quins usuaris poden accedir al ssh.
  Indicarem que només *usuari* pot accedir
  ![allowusers](img/img06.png)
  Creem un usuari secundari anomenat *usuari2*
  ![ceració usuari](img/img05.png)
- Comprovem que es pot connectar remotament a *usuari* però no a *usuari2*
  ![usuari](img/img02.png)
  ![usuari](img/img03.png)
  ![usuari](img/img07.png)

- Configurem amb redirecció dinàmica per redirigir el trànsit.


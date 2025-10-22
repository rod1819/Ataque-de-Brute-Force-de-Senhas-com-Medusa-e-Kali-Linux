# Ataque-de-Brute-Force-de-Senhas-com-Medusa-e-Kali-Linux
**Objetivo**: Neste projeto iremos simular um ataque de senha utilizando o recurso Medusa do Kali Linux.

---
## Conteúdo deste pacote
- `README.md` = Obtém a documentação e a explicação.
- `users.txt` = wordlist de usuários de exemplo.
- `passwords.txt` = wordlist de senhas de exemplo.

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




# ssh_termux

# Tutorial: Como copiar arquivos entre computadores com Ubuntu e um celular com Termux usando SSH

Este tutorial ensinará como copiar arquivos e pastas entre um computador com **Ubuntu** (IP: `192.168.0.117`) e um celular com **Termux** (IP: `192.168.0.144`), utilizando o **SSH**. O Termux está configurado para usar a porta **8022** para conexões SSH.

---

## 📌 Pré-requisitos

### 1. Servidor SSH ativo em ambos os dispositivos

**No Termux:**
```bash
pkg install openssh
sshd
```

**No Ubuntu:**
```bash
sudo apt update
sudo apt install openssh-server
sudo systemctl start ssh
```

### 2. Verificar IPs

**Termux:**
```bash
ifconfig
```
**Debian:**
```bash
ip addr
```

### 3. Liberar acesso ao armazenamento no Termux
```bash
termux-setup-storage
```

### 4. Credenciais de acesso
Tenha usuário e senha do Debian e do Termux.

---

## 1. 📤 Copiar arquivos **do Termux para o Debian**

➡️ **Aqui não é necessário informar porta**, pois o Debian usa a porta padrão `22`.

### Copiar um arquivo
No Termux:
```bash
scp ~/caminho/do/arquivo.ext usuario_debian@192.168.0.117:~/destino/
```

**Exemplo:**
```bash
scp ~/teste.txt andre@192.168.0.117:~/Documentos/
```

### Copiar uma pasta inteira
```bash
scp -r ~/caminho/da/pasta usuario_ubuntu@192.168.0.117:~/destino/
```

**Exemplo:**
```bash
scp -r ~/meusarquivos andre@192.168.0.117:~/Documentos/
```

---

## 2. 📥 Copiar arquivos **do Debian para o Termux**

➡️ Aqui **é obrigatório** informar a porta **8022**, que é a porta do SSH no Termux.

### Copiar um arquivo
No Debian:
```bash
scp -P 8022 ~/caminho/do/arquivo.ext usuario_termux@192.168.0.144:~/destino/
```

**Exemplo:**
```bash
scp -P 8022 ~/teste.txt u0_a123@192.168.0.144:~/storage/downloads/
```

### Copiar uma pasta inteira
```bash
scp -P 8022 -r ~/caminho/da/pasta usuario_termux@192.168.0.144:~/destino/
```

**Exemplo:**
```bash
scp -P 8022 -r ~/Documentos u0_a123@192.168.0.144:~/storage/shared/
```

---

## 3. 🔧 Testando o SSH

### Debian → Termux
```bash
ssh -p 8022 usuario_termux@192.168.0.144
```

### Termux → Debian
```bash
ssh usuario_debian@192.168.0.117
```

Se houver erro, verifique:
- Se o SSH está ativo.
- Se o IP está correto.
- Se o firewall está liberado.
- Usuário e senha.

---

## 4. 📝 Observações importantes
- Certifique-se de que o diretório destino tem permissão de escrita.
- A porta do Termux é **8022**, não 22.
- Você pode configurar autenticação por chave SSH para não precisar digitar senha sempre.

---

Pronto! Agora você já consegue transferir arquivos entre o Debian e o Termux de forma simples usando SSH. 🚀


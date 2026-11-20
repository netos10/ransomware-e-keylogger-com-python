# ransomware-e-keylogger-com-python

-Projeto prático de código de **ransomware** e **keylogger** realizados em ambiente controlado e sem exposição.

CENÁRIOS:
  Ransomware: criptografia e descriptografia de dados e geração de aviso local.
  Keylogger: captura de eventos de teclado, registro periódico e envio via e-mail.

FERRAMENTAS:
  Linguagem Python
  IDE: PyCharm

----------------------------------------------------------------------------------------------

**1. RANSOMWARE:**

É um tipo de malware que bloqueia o acesso a arquivos e sistemas por criptografia e exige pagamento para um resgate. Eu criei uma pasta "test_files" e ela contém 2 arquivos .txt com informações aleatórias (apenas para serem criptografadas). Dentro do código nós temos algumas etapas obrigatórias, como:
  **1 GERAR CHAVE:** temos a ```def gerar_chave()``` gera uma chave criptográfica com ```Fernet.generate_key(```) e salva esses bytes no arquivo ```chave.key```.
  
 **2 CARREGAR CHAVE:** ```def carregar_chave()``` abre ```chave.key``` e retorna o conteúdo da chave para ser usado na criptografia.
  
  **3. CRIPTOGRAFAR:** ```def criptografar_arquivo(arquivo, chave)``` cria um objeto Fernet(chave), lê o arquivo original , cifra os dados com ```f.encrypt(dados)``` e sobrescreve o mesmo arquivo com o resultado cifrado.
  
 **4. ENCONTRAR ARQUIVOS:** ```def encontrar_arquivos(diretorio)``` percorre o diretório e subpastas com ```os.walk(diretorio)``` monta o caminho de cada arquivo com ```os.path.join(raiz, nome)``` e guarda na lista apenas o que não se chama "ransoware.py" e não termina em ".key".
  
 **5. GERAR MENSAGEM:** ```def criar_mensagem())``` Cria ou sobrescreve o arquivo ) ```LEIA ISSO.txt)``` em modo texto e escreve linhas alertando a vítima.

**6. FUNÇÃO PRINCIPAL:** ```def main()``` executa o fluxo principaL, chama ```gerar_chave()``` duas vezes, lê a chave com ```carregar_chave()```, busca os arquivos em ```"test_file"```, chama ```criptografar_arquivo(arquivo, chave)``` para cada item encontrado e chama ```criar_mensagem()```.

Ao executar esse código, os arquivos .txt localizados na pasta text_file foram completamente criptografados. Para descriptografar eles, foi criado o ```descriptografador.py```. Veja a seguir:

**7. CARREGAR CHAVE:** ```def carregar_chave()``` abre chave.key e retorna os bytes da chave que foi usada para cifrar os arquivos.

**8. DESCRIPTOGRAFAR:** ```def descriptografar_arquivo(arquivo, chave)``` instancia ```Fernet(chave)```, lê o arquivo cifrado, reverte o conteúdo com ```f.decrypt(dados)``` e sobrescreve o mesmo arquivo com os dados originais.

 ****9. ENCONTRAR ARQUIVOS (CÓPIA DO 1.4):** ```def encontrar_arquivos(diretorio)``` percorre o diretório e subpastas com ```os.walk(diretorio)``` monta o caminho de cada arquivo com ```os.path.join(raiz, nome)``` e guarda na lista apenas o que não se chama "ransoware.py" e não termina em ".key".**

 **10. REVERSÃO DE CIFRAGEM:** ```def main()``` Carrega a chave via ```carregar_chave()```, lista os arquivos dentro de "test_file" usando ```encontrar_arquivos("test_file")```, chama ```descriptografar_arquivo(arquivo, chave)``` para cada arquivo encontrado.

----------------------------------------------------------------------------------------------------------------------

**2. KEYLOGGER:**

É um tipo de malware que monitora e registra as teclas pressionadas e age de forma discreta. Para isso, criei um arquivo chamado ```keylogger.pyw```, essa extensão ```pyw``` significa que ele vai rodar em segundo plano no Windows.

Fiz um listener de teclado com o módulo ```pynput``` que salva tudo em ```log.txt```, criamos o conjunto IGNORAR para pular teclas modificadoras (shift, ctrl, alt, etc.), colocamos um try para gravar caracteres normais ```(key.char)``` e um except para tratar teclas especiais, quebra de linha, tabulação, marcadores ou ignorando o resto, deixando o listener rodando em loop.
Ele rodou em segundo plano por estar em ```.pyw```, criou o ```log.txt``` e foi registrando tudo o que era digitado, salvando os caracteres normais no try e filtrando as teclas especiais no except.

**2.1 KEYLOGGER_EMAIL:**

No ```.keylogger_email.py```., fizemos uma versão que guarda as teclas numa variável log em memória em vez de escrever direto no arquivo, e manda esse conteúdo por e-mail via SMTP (smtp.gmail.com, porta 587 com TLS) a cada 60 segundos usando Timer:

```.on_press(key)``` try para somar caracteres normais (key.char) na string log, e um except ```.AttributeError```. para tratar algumas teclas especiais.

```.enviar_email()```: Monta a mensagem com o que foi acumulado em log, tenta conectar e autenticar no servidor SMTP para enviar o e-mail (capturando erros num try/except), limpa o log e agenda o próximo envio a 60 segundos com Timer.

-------------------------------------------------------------------------

É importante ter noção de como esses tipos de ataques, por mais simples que pareçam, são discretos e catastróficos quando não há prevenção e defesa. Obrigado por conferir esse projeto, até mais.

  **-Orlando Neto**

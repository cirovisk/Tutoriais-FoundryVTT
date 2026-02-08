### Vantagens:
- Não usa eletron pra funcionar, ou seja, o host não vai deixar um programa a mais aberto (O eletron é um navegador, então se você abrir ele e o seu navegador normal vai ter mais lag).
- Se o mestre precisar dar F5 no foundry dele o servidor não reinicia automaticamente, então os jogadores não vão precisar relogar (útil para jogadores com pc ou net ruins).
- Pode deixar o servidor aberto de maneira mais leve, porquê o servidor node ocupa bem menos memória que deixar o eletron aberto. Útil para quem hosteia na oracle por consequência.

## Pré-requisitos: 
- Node.JS 
  https://nodejs.org/en/download 
	-  Se tá no windows, baixa o arquivo .msi e instala de boa.
	- Se tá no linux, depende da sua distro, mas no site você tem código bash pra instalar independente. 
		- Via NVM:
			`curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
			``nvm install --lts``
			`nvm use --lts` 
- Foundry nodejs
  
Instalação: 
1. Extraia o arquivo para seu diretório de escolha, lembre-se dele

2. 
	1. **No windows:** `node resources/app/main.js --dataPath="COLOQUE_O_CAMINHO_DA_SUA_PASTA_DE_DADOS_AQUI"`
	2. No **Linux:** `node resources/app/main.js --dataPath="COLOQUE_O_CAMINHO_DA_SUA_PASTA_DE_DADOS_AQUI"`
	obs: O caminho deve estar entre **aspas** (especialmente no Windows, caso existam espaços no nome das pastas). Também evite espaços em branco, acentos ou ç no caminho da pasta, essas coisas.

### SÓ PRA WINDOWS:
3. Criando um arquivo .bat (Executável de um clique): Você pode criar um arquivo que, ao ser clicado duas vezes, abre o terminal e executa todo o comando automaticamente.

	1. Abra o Bloco de Notas.
	2. Cole o seguinte código:

		```@echo off
		cd /d "CAMINHO_PARA_A_PASTA_ONDE_O_FOUNDRY_ESTA_INSTALADO"
		node resources/app/main.js --dataPath="COLOQUE_O_CAMINHO_DA_SUA_PASTA_DE_DADOS_AQUI"
		pause
		```
	4. Vá em Arquivo > Salvar Como.
	5. Nomeie como ligar_foundry.bat (qualquer merda que termine em .bat).
	6. Salve na sua área de trabalho.
	7. Agora, basta dar um duplo clique nesse arquivo para iniciar o servidor.

4. Criando um Atalho do Windows: se você não quiser criar um arquivo extra, pode transformar o próprio executável do Node em um atalho configurado
	1. Clique com o botão direito na sua Área de Trabalho e vá em Novo > Atalho.
	2. No local do item, você vai colar o caminho do Node seguido dos argumentos. 
		```"C:\Program Files\nodejs\node.exe" "C:\Caminho\Para\Foundry\resources\app\main.js" --dataPath="C:\Caminho\Para\Dados"```
	3.  Clique em Avançar, dê o nome que você quiser e finalize.
	4. Agora o servidor ligará apenas clicando no ícone criado.

5. Usando o Gerenciador de Tarefas (Para iniciar com o Windows)
	Se o objetivo é que o servidor ligue sozinho sempre que o computador for ligado:
	1. Pressione Win + R, digite shell:startup e dê Enter.
	2. Coloque uma cópia do arquivo .bat (criado no passo 1) dentro dessa pasta que abriu.
	3. O servidor Node.js iniciará automaticamente em segundo plano sempre que você fizer login no Windows.

**Para acessar o servidor como host o padrão é https://localhost:30000 se vc tá no oracle eu não sei o padrão, te vira, mas deve funcionar para VPNs tipo zero tier ou radmin**

### Para o linux:
1. Criando um Script Executável (.sh): Esta é a forma mais simples. Você cria um arquivo que funciona como um "lançador".
	1. Abra o seu editor de texto e cole o seguinte:
		```
		#!/bin/bash
		cd "CAMINHO_PARA_A_PASTA_ONDE_O_FOUNDRY_ESTA_INSTALADO"
		node resources/app/main.js --dataPath="COLOQUE_O_CAMINHO_DA_SUA_PASTA_DE_DADOS_AQUI"
		```
	2.  Salve o arquivo com .sh  (tipo ligaessaporra.sh)
	3.  Dê permissão de execução para o arquivo. No terminal, use: `chmod +x ligar_foundry.sh`
	4. Para ligar o servidor, basta clicar duas vezes no arquivo (e escolher "Executar no Terminal") ou rodar `./ligar_foundry.sh` de onde ele estiver.

2. Você pode criar um comando curto personalizado no seu sistema para que, toda vez que você digitar `foundry` no terminal, o servidor inicie.

	1. Abra o arquivo de configuração do seu shell (geralmente o `.bashrc` ou `.zshrc` na sua pasta Home).
	2. Adicione esta linha ao final do arquivo: `alias foundry='node "CAMINHO/resources/app/main.js" --dataPath="CAMINHO/DATA"'`
	3. Salve o arquivo e atualize o terminal com o comando `source ~/.bashrc` (ou o arquivo que você editou).    
		- Agora, basta digitar `foundry` em qualquer terminal para iniciar o servidor. 

3. Criando um serviço no Systemd (Para rodar sempre em background):
	1. Crie o arquivo do serviço:`sudo nano /etc/systemd/system/foundry.service`
	```
	[Unit]
	Description=Foundry VTT Node.js Server
	
	[Service]
	WorkingDirectory=/CAMINHO/ONDE/ESTA/INSTALADO
	ExecStart=/usr/bin/node resources/app/main.js --dataPath=/CAMINHO/DOS/DADOS
	Restart=always
	User=SEU_USUARIO_AQUI
	
	[Install]
	WantedBy=multi-user.target
	```
	2. Ative o serviço: 
	`sudo systemctl enable foundry`
	`sudo systemctl start foundry`
	3. Pronto, agora vai rodar sempre que você ligar o pc

**Para acessar o servidor como host o padrão é https://localhost:30000 se vc tá no oracle eu não sei o padrão, te vira, mas deve funcionar para VPNs tipo zero tier ou radmin**

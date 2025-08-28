UDEMY - Curso de python 3 do basico ao avançado

configurando o ambiente

início) install python + VSC
	0.1) configure powershell com "set-ExecutionPolicy AllSigned -Force"
	0.2) criar ambiente com "python -m venv venv"
	0.3) ativar ambiente com ".\venv\Scripts\Activate"

a) configuraçoes do VSC - settings.json
	1.1 ) "window.zoomLevel": 4,
	1.2 ) "window.fontSize": 14,
	1.3 ) arquivo python nomeado com letra, numero e udnerline
	1.4 ) "explorer.compactFolders": false,
	1.5 ) verificar shortcuts padroes no VSC
b) install code runner
	2.1) em qual ordem ele executa extensoes? --> set shortcut
	2.2) settings.json -->
		2.2.1) "code-runner.runInTerminal" : true,
		2.2.2) limpar a tela do terminal
			"code-runner.clearPreviousOutput": true 
			code-runner.executorMap { "python": " cls ; python -u" ou "cls &&...}
		2.2.3) cuidado ao selecionar parte do codigo e rodar
		 "code-runner.ignoreSelection": true,
c) instalar omthemes  (darker dracula) 
		default italic
d) instalar extensions:> material icon theme
	 settings vai ter adicionado colorTheme e iconTheme
e) settings--> "python.defaultInterpreterPath":"python"

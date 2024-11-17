## Criar uma nova feature no Git para subdiretórios em sieca.net

Para criar uma nova feature no Git para subdiretórios em sieca.net, siga estes passos:

1. **Crie um novo branch:**
   ```bash
   git checkout -b feature/subdiretorios-sieca
   ```
   Este comando cria um novo branch chamado `feature/subdiretorios-sieca` baseado no branch atual.

2. **Crie o subdiretório no repositório:**
   ```bash
   mkdir sieca.net/projetos
   ```
   Este comando cria um novo subdiretório chamado `projetos` dentro do diretório `sieca.net`.

3. **Adicione o subdiretório ao controle de versão:**
   ```bash
   git add sieca.net/projetos
   ```
   Este comando adiciona o novo subdiretório ao Git para que ele seja rastreado.

4. **Faça um commit das alterações:**
   ```bash
   git commit -m "Criando subdiretório para projetos"
   ```
   Este comando cria um novo commit com a mensagem "Criando subdiretório para projetos".

5. **Envie as alterações para o repositório remoto:**
   ```bash
   git push origin feature/subdiretorios-sieca
   ```
   Este comando envia as alterações do branch `feature/subdiretorios-sieca` para o repositório remoto.

6. **Crie um pull request:**
   Abra um pull request no repositório do sieca.net, solicitando a mesclagem do branch `feature/subdiretorios-sieca` com o branch principal.

7. **Revise o código e faça o merge:**
   Após a revisão do código, você pode mesclar o branch `feature/subdiretorios-sieca` com o branch principal.

**Após a mesclagem, o subdiretório `projetos` estará disponível no repositório sieca.net.**

**Informações adicionais:**

* Você pode usar o comando `git status` para verificar o estado do Git e ver quais arquivos foram modificados.
* Você pode usar o comando `git diff` para ver as diferenças entre os arquivos.
* Você pode usar o comando `git log` para ver o histórico de commits.

**Lembre-se de:**

* Usar mensagens de commit claras e concisas.
* Testar as alterações cuidadosamente antes de enviar para a branch principal.
* Seguir as convenções de nomenclatura do repositório sieca.net.

**Para mais informações sobre o Git, consulte a documentação oficial:**

https://git-scm.com/doc
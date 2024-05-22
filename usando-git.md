Para versionar seu projeto usando GitHub, siga este guia passo a passo. Vamos focar em ser bem didáticos, principalmente com arquivos `.md` (Markdown) que fornecerão instruções claras para começar e manter o projeto atualizado.

### Passo 1: Criar uma conta no GitHub

1. Vá para [GitHub](https://github.com/) e crie uma conta, se ainda não tiver uma.
2. Confirme seu e-mail e complete o processo de configuração da conta.

### Passo 2: Clonar o repositório existente

1. Acesse o repositório [renato71amorim/estagiario](https://github.com/renato71amorim/estagiario.git).
2. No canto superior direito, clique no botão verde "Code" e copie o link do repositório (usando HTTPS ou SSH).

![Clone repository](https://docs.github.com/assets/images/help/repository/https-url-clone.png)

3. Abra seu terminal (Git Bash, CMD, PowerShell, etc.) e navegue até o diretório onde deseja clonar o repositório.
4. Use o comando abaixo para clonar o repositório:
   ```sh
   git clone https://github.com/renato71amorim/estagiario.git
   ```

### Passo 3: Navegar para o repositório clonado

1. Após clonar o repositório, navegue até o diretório clonado:
   ```sh
   cd estagiario
   ```

### Passo 4: Criar e editar arquivos `.md`

Vamos criar alguns arquivos `.md` essenciais para ajudar novos contribuidores a começar.

#### 1. Criar um arquivo README.md

O `README.md` fornece uma visão geral do projeto, instruções de configuração e uso.

Crie o arquivo `README.md`:
```sh
touch README.md
```

Abra e edite `README.md` com o seguinte conteúdo:

```markdown
# Estagiário

Bem-vindo ao projeto Estagiário! Este repositório contém um conjunto de scripts e ferramentas para auxiliar novos estagiários em seu trabalho diário.

## Como começar

1. Clone o repositório:
   ```sh
   git clone https://github.com/renato71amorim/estagiario.git
   cd estagiario
   ```

2. Instale as dependências (se houver):
   ```sh
   # Exemplo para projetos Node.js
   npm install
   ```

3. Execute o projeto:
   ```sh
   # Comando para iniciar o projeto
   npm start
   ```

## Contribuindo

Para contribuir com o projeto, siga os passos abaixo:

1. Crie uma branch para sua feature ou correção:
   ```sh
   git checkout -b minha-feature
   ```

2. Faça suas mudanças e comite:
   ```sh
   git commit -am "Descrição das mudanças"
   ```

3. Envie sua branch para o repositório remoto:
   ```sh
   git push origin minha-feature
   ```

4. Abra um Pull Request no GitHub.

## Manter o projeto atualizado

Para manter seu fork sincronizado com o repositório original:

1. Adicione o repositório original como um remoto:
   ```sh
   git remote add upstream https://github.com/renato71amorim/estagiario.git
   ```

2. Busque as atualizações do repositório original:
   ```sh
   git fetch upstream
   ```

3. Mescle as atualizações na sua branch principal:
   ```sh
   git checkout main
   git merge upstream/main
   ```

## Licença

Este projeto está licenciado sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.
```

#### 2. Criar um arquivo CONTRIBUTING.md

O `CONTRIBUTING.md` fornece diretrizes sobre como contribuir para o projeto.

Crie o arquivo `CONTRIBUTING.md`:
```sh
touch CONTRIBUTING.md
```

Abra e edite `CONTRIBUTING.md` com o seguinte conteúdo:

```markdown
# Contribuindo para o projeto Estagiário

Obrigado por considerar contribuir para o projeto Estagiário!

## Como contribuir

1. Faça um fork do repositório.
2. Crie uma branch para sua contribuição:
   ```sh
   git checkout -b minha-contribuicao
   ```
3. Faça suas mudanças.
4. Commit suas mudanças:
   ```sh
   git commit -am "Descrição das mudanças"
   ```
5. Envie sua branch para o seu fork:
   ```sh
   git push origin minha-contribuicao
   ```
6. Abra um Pull Request no repositório original.

## Código de Conduta

Por favor, siga o nosso [Código de Conduta](CODE_OF_CONDUCT.md) ao interagir com a comunidade do projeto.
```

### Passo 5: Comitar e enviar mudanças

1. Adicione os novos arquivos ao controle de versão:
   ```sh
   git add README.md CONTRIBUTING.md
   ```

2. Faça o commit das mudanças:
   ```sh
   git commit -m "Adiciona arquivos README e CONTRIBUTING"
   ```

3. Envie as mudanças para o repositório remoto:
   ```sh
   git push origin main
   ```

### Conclusão

Agora, seu repositório está configurado com instruções claras sobre como começar, contribuir e manter o projeto atualizado. Esses arquivos `.md` ajudarão a garantir que todos os colaboradores tenham um entendimento claro do fluxo de trabalho e das expectativas do projeto.
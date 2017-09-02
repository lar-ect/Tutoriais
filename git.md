### Remover arquivo que já foi commitado

***

Remove o arquivo e adiciona ao .gitignore para que ele não seja mais detectado pelo git
```
git rm --cached nome_do_arquivo
echo "nome_do_arquivo" >> .gitignore
```

### Adicionar as mudanças locais a um branch e voltar a versão anterior do projeto

***

**Exemplo:** Você está trabalhando em uma nova funcionalidade mas o código está muito diferente do código original e você precisa voltar ao original para corrigir um bug

Cria um novo branch, adiciona todos os arquivos modificados, faz o commit e faz o push para o github:
```
git checkout -b nome_do_novo_branch
git add .
git commit -m "Mensagem do commit"
git push --set-upstream origin nome_do_novo_branch
```
### Reverter informações sensitivas de um commit que já foi enviado ao github.

***

**Exemplo:** Você enviou a senha do banco de dados para o github em um commit e deseja remover tal senha.

Primeiramente, encontre a chave do commit que você deseja alterar utilizando o comando `git log`:

```
git log

commit a56686b9719592a102b95ed14d825306aea5362b
Author: Gabriel Tibúrcio <tibuurcio@gmail.com>
Date:   Fri Aug 25 15:53:58 2017 -0300

    feat(analytics): Adiciona o google analytics quando NODE_ENV=production
```

A chave do commit são os 7 primeiros caracteres `a56686b`

Em seguida, utilize o comando `rebase` utilizando a flag `--interactive` e a chave do commit:

```
git rebase --interactive a56686b
```

Isso irá abrir um arquivo de texto em seu editor de texto padrão, digite o seguinte:

```
edit a56686b Mensagem de edição do rebase
```

Após isso, modifique as linhas que você quer remover dos arquivos alterados e depois commit as alterações:

```
git commit --all --amend --no-edit
git rebase --continue
```

Para finalizar, envie as alterações para o github:

```
git push -f origin master
```

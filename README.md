# flow-show

### Github git flow

Esse exercício servirá para mostrar o fluxo que devemos seguir durante nosso desenvolvimento

utilizando o git e um projeto sério compartilhado com um time de desenvolvedores.

### Cola do fluxo

0. `git checkout {o projeto git}`

1. Navegue até a pasta do projeto e puxe a última versão do branch `develop` (não fazer isso gerará mais trabalho para você mesmo no futuro):

`git pull origin develop`

2. Crie um novo branch para sua funcionalidade (você pode escrever seu código ainda na `develop` mas antes de qualquer commit crie seu branch

ou precisará migrar seus commits para outro branch utilizando provavelmente `git apply` ou `git cherry-pick` - você NÃO pusha conteúdo para os

branchs `develop` e `master`!!!!!!!!)

`git checkout -b {suas duas iniciais + nome da funcionalidade -> a minha poderia ser tf-minha-funcionalidade}`

3. Faça o que precisar e o que quiser com sua branch desde que não afete o histórico herdado da branch `develop`

4. Quando estiver com a funcionalidade pronta você tem dois caminhos:

4.1 Fazer seus commits na branch local da funcionalidade (se quiser pode inclusive pushar elas para o github, sem problemas - ainda é apenas

sua branch de trabalho)

4.2 Fazer todas as suas modificaçōes de uma vez, sem commits (mais perigoso pois não te dá um histórico nem pontos a que você pode voltar se quebrar

o próprio desenvolvimento) e depois fazer um `git stash` para que ele guarde todas as suas modificaçōes e retorne o código à sua base (provavelmente

ao `develop` inicial em que você iniciou o desenvolvimento)

5. Volte para o branch `develop` e dê um pull na última versão

```bash
git checkout develop
git pull origin develop
```

6. Vá para seu branch da feature, no meu caso com

`git checkout tf-minha-funcionalidade`

e faça um rebase para a última versão da `develop`, o que irá transportar a base do seu branch para a última versão atualizada da `develop` fazendo com que

suas mudanças sejam aplicadas sobre o código mais novo vigente para o time

`git rebase develop`

7. Isso gera dois fluxos dependendo de sua escolha em `4`:

7.1 Caso você tenha optado pelo caminho `4.1` ao fazer o rebase o git irá aplicar os commits feitos em sua branch sobre a nova versão da `develop`

o que potencialmente gerará conflitos. A cada conflito ele irá reclamar que não conseguiu fazer um merge de certo arquivo (e te mostrar o arquivo)

então basta que você edite o arquivo, resolva os conflitos depois retorne à linha de comando e readicione aquele arquivo ao git (para que ele saiba

que o conflito foi resolvido) com o `git add {nome do arquivo}`. Após resolver todos os problemas diga ao git que ele pode continuar o rebase para aplicar

seus commits até o fim

`git rebase --continue`

Se ele disser que o rebase terminou ou que não há rebase em andamento você terminou de fazer o rebase e o merge.

7.2 Se você seguiu o caminho `4.2` diga ao git para aplicar as mudanças que ele guardou sobre seu branch

`git stash apply`

isso potencialmente gerará conflitos, resolva-os, dê add e comite tudo o que quer adicionar e submeter com seu branch

8. Teste seu branch, rode testes, use-o, cheque se sua funcionalidade funciona sem que você tenha quebrado funcionalidades alheias com seus merges.

Pode fazer mais commits em cima de seu branch (e outros rebases no futuro) e quando estiver pronto faça um push dele para o github

`git push origin {nome da sua branch - no meu caso seria tf-minha-funcionalidade}`

## Atenção:

Se você já havia feito um push de sua branch para o github e depois fez o rebase ele irá reclamar que o branch local e o remoto diferem,

para resolver você deverá sobrescrever o branch remoto com sua versão (que deve ser a atual e correta!) utilizando

`git push --force origin {nome da sua branch - no meu caso seria tf-minha-funcionalidade}`

Isso irá sobrescrever sua branch remota e o que havia lá não poderá ser recuperado, então garanta que seu branch local está correto!

### Pull Request

Há alguns meios de se abrir uma PR no github mas no geral eles seguem o padrão:

1. Vá à sessão de branches do repositório

2. Clique no botão `Pull Request` na linha de seu branch

1.a Navegue até sua branch no repositório (pode ser feito ou clicando no nome de sua branch ou no select da página inicial do projeto selecione o nome de sua branch)

2.a Aperte o botãozinho verde ao lado do select de branches com o simbolo de PR

3. Cheque que a branch selecionado no select `base` é a `develop` e a sua branch está na select `compare` (se estiver correto a página deve conter apenas

uma lista dos seus commits no seu branch e no diff apresentado devem haver todas e apenas as suas modificaçōes)

4. Entre uma mensagem descrevendo o conteúdo da funcionalidade implementada e o que foi feito na branch, pode marcar pessoas, fazer perguntas,

pedir para alguem checar algo etc. Isso quer dizer que você acha que terminou o trabalho, não quer dizer que não vai ter que fazer modificaçōes.

5. Clique em `Create Pull Request` (o botão verde abaixo da área de mensagem)


### Mais informaçōes

[Entenda alguns fluxos de git e o porquê não utilizaremos o fluxo centralizado](https://www.atlassian.com/git/tutorials/comparing-workflows/centralized-workflow)



# QuizIA – quiz multiplayer ao vivo sobre Inteligência Artificial

Site estático (HTML + CSS + JavaScript) que funciona como um mini-Kahoot: o apresentador cria uma sala, mostra o QR code no projetor e os participantes respondem pelo celular, sem cadastro.

Tudo é **gratuito**: Firebase (plano Spark, sem cartão de crédito) e GitHub Pages. Você não precisa de terminal, Node.js nem de instalar nada.

Os três arquivos do projeto:

| Arquivo | Para que serve |
|---|---|
| `index.html` | O site inteiro (telas, jogo, perguntas). |
| `database.rules.json` | Regras de segurança que você cola no Firebase. |
| `LEIA-ME.md` | Este tutorial. |

> Os passos marcados com **👉 Você faz** precisam ser feitos por você, com a sua conta. Nada está publicado ainda: o site só vai existir depois que você concluir os passos abaixo.

---

## Passo 1 – Criar o projeto no Firebase

👉 **Você faz:**

1. Entre em <https://console.firebase.google.com> com sua conta Google.
2. Clique em **Criar um projeto** (ou **Adicionar projeto**).
3. Dê um nome, por exemplo `quizia-seunome`, e clique em **Continuar**.
4. Se perguntar sobre o Google Analytics, pode **desativar** (não é necessário). Clique em **Criar projeto** e aguarde.
5. Quando terminar, clique em **Continuar**.

O plano padrão é o **Spark (gratuito)**. Você não precisa informar cartão de crédito. Não faça upgrade para o plano Blaze.

## Passo 2 – Ativar o Realtime Database

👉 **Você faz:**

1. No menu da esquerda, abra **Criação** (ou **Build**) e clique em **Realtime Database**.
2. Clique em **Criar banco de dados**.
3. Escolha a localização (pode deixar a sugerida, por exemplo *Estados Unidos*).
4. Escolha **Iniciar no modo bloqueado** e clique em **Ativar**.
5. Na tela do banco, **copie o endereço** que aparece no topo, parecido com `https://quizia-seunome-default-rtdb.firebaseio.com` (ou `...europe-west1.firebasedatabase.app`). Você vai usá-lo no Passo 5.

## Passo 3 – Ativar o login anônimo

É isso que identifica cada celular sem pedir e-mail ou senha.

👉 **Você faz:**

1. No menu da esquerda, abra **Criação → Authentication** e clique em **Vamos começar**.
2. Na aba **Método de login** (Sign-in method), clique em **Anônimo**.
3. Ative a chave **Ativar** e clique em **Salvar**.

## Passo 4 – Colar as regras de segurança

👉 **Você faz:**

1. Volte em **Realtime Database** e abra a aba **Regras**.
2. Apague todo o conteúdo que estiver na caixa.
3. Abra o arquivo `database.rules.json`, copie **tudo** e cole na caixa.
4. Clique em **Publicar**.

O que essas regras garantem:

- Só quem criou a sala (o usuário anônimo do apresentador) altera o estado da partida, as perguntas e o placar.
- Cada participante só escreve o **próprio** apelido e a **própria** resposta, uma única vez por pergunta.
- Respostas fora do tempo, ou com a rodada encerrada, são recusadas pelo banco.
- O gabarito fica em `rooms/CÓDIGO/keys`, que **só o apresentador consegue ler**. A resposta certa só aparece para os jogadores quando o apresentador clica em *Revelar resposta*.
- Os participantes não conseguem ler as respostas dos outros.
- Não existe regra aberta para o banco inteiro.

## Passo 5 – Copiar a configuração do Firebase para o `index.html`

👉 **Você faz:**

1. No Firebase, clique na engrenagem ⚙️ ao lado de **Visão geral do projeto** → **Configurações do projeto**.
2. Role até **Seus apps** e clique no ícone **`</>`** (Web).
3. Dê um apelido (por exemplo `quizia-web`). **Não** marque *Firebase Hosting*. Clique em **Registrar app**.
4. Aparecerá um bloco de código com `const firebaseConfig = { ... }`. Deixe essa janela aberta.
5. Abra o `index.html` no **Bloco de Notas** (Windows), **TextEdit** (Mac, em modo texto simples) ou editor de código. Procure por `COLE_AQUI`. Você verá:

```js
const firebaseConfig = {
  apiKey: "COLE_AQUI_apiKey",
  authDomain: "COLE_AQUI_authDomain",
  databaseURL: "COLE_AQUI_databaseURL",
  projectId: "COLE_AQUI_projectId",
  storageBucket: "COLE_AQUI_storageBucket",
  messagingSenderId: "COLE_AQUI_messagingSenderId",
  appId: "COLE_AQUI_appId"
};
```

6. Substitua cada valor pelo correspondente do Firebase, **mantendo as aspas**.
7. Se o bloco do Firebase **não** tiver `databaseURL`, use o endereço copiado no Passo 2.
8. Salve o arquivo.

Se você deixar algum `COLE_AQUI`, o site mostra um aviso “Falta configurar o Firebase” em vez de funcionar.

## Passo 6 – Autorizar o domínio do GitHub Pages (faça depois do Passo 8)

Quando souber o endereço do seu site (Passo 8), faça:

👉 **Você faz:** no Firebase, **Authentication → Configurações → Domínios autorizados → Adicionar domínio** e digite `seu-usuario.github.io` (somente o domínio, sem `https://` e sem o nome do repositório).

## Passo 7 – Criar o repositório no GitHub e enviar os arquivos (sem terminal)

👉 **Você faz:**

1. Crie uma conta em <https://github.com> (gratuita), se ainda não tiver.
2. Clique em **+** (canto superior direito) → **New repository**.
3. Nome: por exemplo `quizia`. Marque **Public**. Clique em **Create repository**.
4. Na página do repositório, clique em **uploading an existing file** (ou **Add file → Upload files**).
5. Arraste os três arquivos (`index.html` já com a sua configuração, `database.rules.json` e `LEIA-ME.md`).
6. Clique em **Commit changes**.

O arquivo precisa se chamar exatamente `index.html`, na raiz do repositório.

## Passo 8 – Ativar o GitHub Pages

👉 **Você faz:**

1. No repositório, clique em **Settings** (Configurações) → **Pages** (menu da esquerda).
2. Em **Build and deployment → Source**, escolha **Deploy from a branch**.
3. Em **Branch**, escolha `main` e a pasta `/ (root)`. Clique em **Save**.
4. Aguarde de 1 a 3 minutos e atualize a página. Aparecerá o endereço, no formato `https://seu-usuario.github.io/quizia/`.
5. Agora volte ao **Passo 6** e autorize o domínio no Firebase.

## Passo 9 – Testar o jogo

👉 **Você faz:**

1. Abra o endereço publicado no computador e clique em **Criar sala**.
2. Em **outro aparelho** (celular) ou em uma **janela anônima/privada** do navegador, abra o mesmo endereço, digite o código e um apelido.
3. Repita com um segundo participante, em outro celular ou outra janela anônima.
4. No computador, confira se os apelidos aparecem. Clique em **Iniciar quiz**.
5. Responda nos celulares, clique em **Encerrar rodada** e depois em **Revelar resposta**. Veja a correção e a pontuação nos celulares e o ranking no computador.
6. Avance até o fim para ver o pódio. Use **Jogar de novo** (ou **Reiniciar partida**) para recomeçar.

> **Importante:** abas comuns do mesmo navegador compartilham o mesmo login anônimo. Se você abrir o apresentador e o participante em duas abas normais, o Firebase enxerga a mesma pessoa. Para testar no mesmo computador, use uma **janela anônima** ou outro navegador. O ideal é usar celulares.

## Passo 10 – Gerar e testar o QR code com o endereço real

👉 **Você faz:**

1. Abra o site **pelo endereço publicado** (`https://seu-usuario.github.io/quizia/`) e clique em **Criar sala**.
2. O QR code é gerado automaticamente com o endereço real da página mais `?sala=CÓDIGO`. Ele só fica correto quando você abre o site pelo endereço publicado, nunca pelo arquivo no seu computador.
3. Aponte a câmera de um celular para o QR code. A página deve abrir com o código já preenchido; falta só digitar o apelido.
4. Teste também o botão **Copiar link** e cole o link no navegador de um celular.
5. Antes da apresentação, teste o QR code na tela do projetor, à distância em que o público estará.

---

## Como editar as perguntas e o tempo

No `index.html`, procure por `const QUIZ = [`. Cada pergunta tem:

- `text`: o enunciado;
- `options`: as 4 alternativas;
- `correct`: a posição da certa (`0` = A, `1` = B, `2` = C, `3` = D);
- `explain`: a explicação curta;
- `time`: tempo padrão, em segundos.

O apresentador também pode mudar o tempo de cada pergunta (de 5 a 180 s) no campo ao lado do botão que inicia a pergunta. Se mudar as perguntas, envie o `index.html` de novo ao GitHub (**Add file → Upload files**, mesmo nome, e confirme a substituição) e crie uma sala nova.

## Como a pontuação funciona

Resposta errada ou ausente vale 0. Resposta certa vale de **500 a 1000 pontos**: quanto mais rápido, mais pontos. O tempo é medido pelo relógio do servidor do Firebase (`serverTimestamp`), então diferenças de relógio entre celulares não afetam o resultado. O apresentador calcula tudo de uma vez ao revelar a resposta.

## Segurança: o que você precisa saber

- **A configuração do Firebase no `index.html` é pública por natureza.** Qualquer pessoa que abrir o site consegue ver `apiKey`, `projectId` etc. Isso é normal e esperado para aplicativos web. Essa chave só identifica o projeto, não dá acesso de administrador.
- **O que protege seus dados são as regras** (`database.rules.json`). Por isso o Passo 4 é essencial. Nunca deixe o banco em “modo de teste” e nunca use regras com `".read": true` e `".write": true` na raiz.
- Nunca cole no `index.html` chaves privadas, contas de serviço ou senhas de administrador. Este projeto não usa nenhuma.
- **Limite honesto:** como o repositório é público, o gabarito das perguntas também aparece no código do `index.html`. As regras impedem que os jogadores leiam a resposta pelo *banco de dados* antes da revelação, mas um participante técnico que abrir o código-fonte do site poderia ver as respostas. Para uma apresentação descontraída isso é aceitável. Para uma prova séria, seria necessário um servidor.
- Opcional, para quem quer ir além: no Google Cloud Console (APIs e serviços → Credenciais) você pode restringir a chave de API para aceitar apenas o seu domínio `seu-usuario.github.io/*`.

## Limites do plano gratuito

O plano Spark do Firebase tem limites (por exemplo, cerca de 100 conexões simultâneas no Realtime Database), suficientes para uma sala de aula ou uma palestra pequena. Se precisar de mais gente, consulte os limites atuais na página de preços do Firebase. As salas antigas não são apagadas sozinhas: de vez em quando, apague o nó `rooms` em **Realtime Database → Dados** para limpar.

## Problemas comuns

| Sintoma | O que fazer |
|---|---|
| Tela “Falta configurar o Firebase” | Ainda há `COLE_AQUI` no `index.html`. Refaça o Passo 5 e envie o arquivo de novo ao GitHub. |
| “Login anônimo não está ativado” | Refaça o Passo 3. |
| Erro de domínio não autorizado | Refaça o Passo 6. |
| `PERMISSION_DENIED` | As regras não foram publicadas ou foram coladas incompletas. Refaça o Passo 4. |
| Página em branco ou erro de conexão | Abra pelo endereço `https://...github.io/...`, não clicando duas vezes no arquivo. |
| Mudei o arquivo e nada mudou | Aguarde 1–2 minutos e recarregue com **Ctrl+F5** (ou limpe o cache do celular). |
| QR code não aparece | Confira a internet (a biblioteca do QR vem da internet) e use o botão **Copiar link** como alternativa. |
| “Sala não encontrada” | Confira o código (sem espaços; letras O e 0 não são usadas) e se a sala foi criada neste mesmo projeto. |

Bom jogo e boa apresentação! 🚀

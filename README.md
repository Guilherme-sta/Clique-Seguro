# Clique Seguro

Simulador educativo de ameaças digitais em formato de navegador, desenvolvido como **Projeto Integrador** do curso Técnico em Informática integrado ao Ensino Médio.

O jogador navega por um ambiente fictício (buscador, e-mail, fórum, downloads e uma plataforma de jogos) e encontra, durante atividades normais, armadilhas como phishing, malvertising, homógrafos, extensões maliciosas e engenharia social. O aprendizado vem da **interação, dos indícios visíveis e das consequências**, e não de um quiz.

> Todo o conteúdo é fictício e roda localmente no navegador. Nenhuma ameaça é executada de verdade.

## Objetivo

Desenvolver o raciocínio crítico sobre segurança digital: ler URLs, interpretar certificados, avaliar remetentes, decidir sobre downloads e permissões, e responder a incidentes. O jogo também inclui casos **legítimos** que parecem suspeitos, para ensinar análise por evidências e não desconfiança indiscriminada.

## Público-alvo

Estudantes do 3º ano do Ensino Médio integrado ao Curso Técnico em Informática.

## Como executar

O projeto é um **único arquivo HTML**, sem dependências e sem instalação.

1. Baixe ou clone o repositório.
2. Abra `index.html` em um navegador moderno (Chrome, Edge, Firefox ou Safari).

Para publicar no GitHub Pages, ative **Settings → Pages** e escolha a branch principal.

## Como jogar

- Você começa no buscador **Seeker**. A missão é encontrar o evento de aniversário da plataforma fictícia **Blockverse** e resgatar as Gemas sem comprometer a conta.
- Use as ferramentas do navegador: passe o mouse sobre os links (a barra de status mostra o destino real), abra o cadeado para ver o certificado, use o botão **⚑ Denunciar** e o menu **☰**.
- A **integridade da conta** cai a cada incidente. Em 0%, a conta é perdida.
- Ctrl, Cmd ou Shift + clique em um link abre em nova aba.
- Os dados de login são fictícios e já vêm preenchidos (`aluno_demo`).

## Recursos

- Navegador simulado com abas, barra de endereço editável com sugestões, voltar, avançar, recarregar e página inicial.
- Buscador com sugestões automáticas e resultados com anúncios patrocinados.
- E-mail (SeekerMail) com cabeçalhos, links e anexos.
- Fórum e **gerenciador de downloads** (assinatura, verificação de SHA-256, executar ou excluir).
- Gerenciador de **permissões** e **extensões**.
- Plataforma Blockverse: perfil, inventário, mensagens, trocas e ajuda.
- **Campanha em 6 fases** com objetivos e liberação por progresso.
- **Motor de eventos** (notificações por fase) e **registro de eventos**.
- **Modo Detetive:** ferramentas de análise, registro de evidências e conclusão (malicioso ou legítimo).
- **Glossário** técnico e **Central de segurança**.
- Relatório final com pontuação por competência e classificação.
- Progresso salvo no navegador (`localStorage`).
- Tema claro e escuro, navegação por teclado e respeito a `prefers-reduced-motion`.

## Ameaças simuladas

| Técnica | Onde aparece |
|---|---|
| Malvertising e janela de login falsa (*browser-in-the-browser*) | Anúncio do gerador de Gemas |
| Abuso de notificações do navegador | Pop-up falso de "não sou robô" |
| Typosquatting e homógrafo via link encurtado | Link do "amigo" e página de login falsa |
| Executável com *infostealer* | Programa "Boost" do fórum |
| Scareware (falso alerta de vírus) | Pop-up com "X" falso |
| Engenharia social contra o 2FA | Mensagem de falso moderador |
| Spear phishing por e-mail | E-mail com anexo `.pdf.exe` |
| Instalador falso por malvertising | Falso "Studio Launcher" |
| Extensão maliciosa com permissões excessivas | Extensão "Gem Helper" |
| Oferta de troca fraudulenta | Mensagem de usuário recente |

## Estrutura do código

Tudo está em `index.html` (HTML, CSS e JavaScript). Os dados dos cenários ficam separados da lógica:

| Estrutura | Função |
|---|---|
| `P` | Catálogo de páginas (URL, certificado, HTML, ameaça associada) |
| `T` | Catálogo de ameaças (indícios, impacto e estado) |
| `DM` | Mapa de endereços digitados para páginas |
| `DLS` | Downloads (origem, assinatura, hash) |
| `DC` | Casos do Modo Detetive |
| `PH` | Fases da campanha e condições de conclusão |
| `EV` | Eventos e notificações por fase |
| `GL` | Glossário |
| `ACT` | Ações de interface (`data-a="acao:parametro"`) |

### Adicionando um cenário

```js
// 1. Ameaça
T.t12 = { n: "Nome da ameaça", w: ["indício 1", "indício 2"], x: ["impacto 1"] };

// 2. Página
P.minhapagina = {
  u: "https://exemplo-falso.test/pagina",
  t: "Título da aba",
  c: ["Emissor", "Tipo de validação", "registrado há 3 dias", "Organização"],
  tr: "t12",
  h: '<div class="bd">... ' + L("outra", "https://destino.test", "link") + '</div>'
};

// 3. Endereço digitável (opcional)
DM["exemplo-falso.test"] = "minhapagina";
```

Cuidados importantes:

- Defina `ACT.nome = ...` **depois** de `var ACT = {...}`.
- O caractere `о` (U+043E, cirílico) em `blоckverse.com` é intencional. Não normalize esse texto.

## Segurança e ética

- Nenhuma credencial real é usada (`aluno_demo` e `senha-demo` são fictícios).
- Nada é enviado para servidores externos e nenhum arquivo é executado.
- As consequências são apenas simuladas dentro do jogo.
- O único link externo é o do formulário de avaliação, exibido na tela final.
- Nomes e marcas são fictícios (Blockverse, Gemas, Seeker). Não há afiliação com serviços reais.

## Status e limitações

- Verificado com checagem de sintaxe e simulações da lógica. **Ainda sem testes formais em navegadores reais e em celulares.**
- Poucos casos de Detetive e poucos eventos por fase (os eventos ainda são fixos por fase).
- Ainda não há conquistas, histórico de navegação em tela, pré e pós-teste nem painel para professores.
- Tudo está em um único arquivo. Se o projeto crescer, a ideia é modularizar.

## Avaliação do projeto

Ao final do jogo, um QR Code leva ao formulário de avaliação do Projeto Integrador:
https://forms.gle/ken7KfseB81egaa48

# 🎲 Gerador de Conselhos (Advice Generator App) - Frontend Mentor

Esta é uma solução para o desafio [Advice generator app do Frontend Mentor](https://www.frontendmentor.io/challenges/advice-generator-app-Qd1A32p2a)[cite: 4]. Os desafios do Frontend Mentor ajudam a aprimorar suas habilidades de desenvolvimento web criando projetos do mundo real.

---

## 📋 Sumário

- [Visão Geral](#visão-geral)
  - [O Desafio](#o-desafio)
  - [Capturas de Tela](#capturas-de-tela)
  - [Links](#links)
- [Meu Processo](#meu-processo)
  - [Tecnologias Utilizadas](#tecnologias-utilizadas)
  - [Funcionalidades e Estilização](#funcionalidades-e-estilização)
  - [Sugestão de Integração com JavaScript](#sugestão-de-integração-com-javascript)
- [Autor](#autor)
- [Agradecimentos](#agradecimentos)

---

## 🔍 Visão Geral

### 🎯 O Desafio

Os usuários devem ser capazes de:

- Visualizar o layout ideal para a aplicação dependendo do tamanho da tela do dispositivo (Desktop/Mobile).
- Ver os estados de foco/hover para todos os elementos interativos na página.
- Gerar um novo conselho aleatório ao clicar no ícone do dado (requer integração com a API [Advice Slip API](https://api.adviceslip.com/)).

### 📸 Capturas de Tela

| Layout Desktop | Estado Ativo (Hover) |
|:--------------:|:--------------------:|
| ![Design Desktop](./desktop-design.jpg) | ![Estado Ativo](./active-states.jpg) |

### 🔗 Links

- **URL da Solução:** [Adicione o link do seu repositório aqui](https://github.com/seu-usuario/seu-repositorio)
- **URL do Site Online:** [Adicione o link do seu site publicado aqui](https://seu-usuario.github.io/seu-repositorio)

---

## 🛠️ Meu Processo

### 🧱 Tecnologias Utilizadas

- **HTML5**: Estruturação semântica e acessibilidade.
- **CSS3**: Uso de variáveis CSS (`:root`), alinhamento com Flexbox e efeitos de transição/sombra[cite: 5].
- **Google Fonts**: Tipografia [Manrope](https://fonts.googleapis.com/css2?family=Manrope:wght@800&display=swap)[cite: 5].
- **Advice Slip API**: *(Recomendada para consumo assíncrono dos conselhos)*.

### 🌟 Funcionalidades e Estilização

- **Centralização do Layout**: Utilização de Flexbox no `body` e no cartão de mensagem (`#messageBox`) para alinhamento centralizado na tela[cite: 5].
- **Efeito Glow no Botão**: Efeito de brilho customizado com `box-shadow` ao passar o ponteiro do mouse sobre o botão de dado (`.button:hover`)[cite: 5].
- **Variáveis de Design**: Uso de variáveis para gerenciar a paleta de cores (`--backgroundColor`, `--backgroundButton`, `--colorTxt`)[cite: 5].

---

## 💡 Sugestão de Integração com JavaScript

Atualmente, o arquivo HTML apresenta um conselho estático (`ADVICE #117`)[cite: 4]. Para tornar a aplicação totalmente funcional consumindo conselhos em tempo real da **Advice Slip API**, você pode criar um arquivo `script.js` com o seguinte código:

```javascript
// Seleção dos elementos do DOM
const adviceId = document.querySelector("#messageBox h1");
const adviceText = document.querySelector("#messageBox p");
const diceBtn = document.querySelector(".button");

// Função para buscar conselho da API
async function buscarConselho() {
  try {
    adviceText.textContent = "Carregando conselho...";
    const response = await fetch("[https://api.adviceslip.com/advice](https://api.adviceslip.com/advice)");
    
    if (!response.ok) {
      throw new Error(`Erro na requisição: ${response.status}`);
    }

    const data = await response.json();
    
    // Atualiza a interface com o ID e o texto do conselho
    adviceId.textContent = `ADVICE #${data.slip.id}`;
    adviceText.textContent = `"${data.slip.advice}"`;
  } catch (error) {
    console.error("Erro ao buscar conselho:", error);
    adviceText.textContent = "Ops! Não foi possível carregar um conselho agora. Tente novamente.";
  }
}

// Evento de clique no botão do dado
diceBtn.addEventListener("click", buscarConselho);

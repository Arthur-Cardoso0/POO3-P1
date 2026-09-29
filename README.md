# FilmFlix — Sistema Web de Controle de Cinema

Sistema web para gerenciamento de cinema desenvolvido com HTML, Bootstrap e JavaScript puro. Permite cadastrar filmes, salas e sessões, além de realizar a venda de ingressos com controle de ocupação em tempo real.

---

##  Sobre o Projeto

Projeto desenvolvido como trabalho prático da disciplina de POO3, com foco em manipulação do DOM, armazenamento local via `localStorage` e encadeamento de dados entre entidades.

---

##  Funcionalidades

- **Cadastro de Filmes** — título, gênero, descrição, classificação indicativa, duração e data de estreia
- **Cadastro de Salas** — nome, capacidade e tipo (2D, 3D ou IMAX)
- **Cadastro de Sessões** — vincula filme e sala, define data/hora, preço, idioma e formato
- **Venda de Ingressos** — seleciona sessão, registra cliente, CPF, assento e forma de pagamento
- **Listagem de Sessões** — exibe todas as sessões disponíveis com barra de ocupação e bloqueio automático quando lotadas
- **Menu fixo** em todas as páginas para navegação rápida

---

##  Estrutura de Arquivos

```
FilmFlix/
├── index.html               # Página inicial
├── cadastro-filmes.html     # Formulário de cadastro de filmes
├── cadastro-salas.html      # Formulário de cadastro de salas
├── cadastro-sessoes.html    # Formulário de cadastro de sessões
├── sessoes.html             # Listagem de sessões disponíveis
├── venda-ingressos.html     # Formulário de venda de ingressos
├── css/
│   ├── bootstrap.min.css    # Framework Bootstrap
│   └── style.css            # Estilos customizados
└── js/
    ├── bootstrap.bundle.min.js
    └── main.js              # Lógica central: DB helper + menu de navegação
```

---

##  Tecnologias Utilizadas

| Tecnologia | Uso |
|---|---|
| HTML5 | Estrutura das páginas |
| CSS3 + Bootstrap 5 | Estilização e responsividade |
| JavaScript (ES6+) | Lógica, DOM e armazenamento |
| localStorage | Persistência de dados no navegador |

---

##  Armazenamento de Dados

Os dados são persistidos no `localStorage` do navegador, organizados nas seguintes chaves:

| Chave | Conteúdo |
|---|---|
| `filmes` | Array de objetos com os filmes cadastrados |
| `salas` | Array de objetos com as salas cadastradas |
| `sessoes` | Array de objetos com as sessões (vinculam filmes e salas) |
| `ingressos` | Array de objetos com as vendas realizadas |

Todos os dados são serializados com `JSON.stringify()` ao salvar e desserializados com `JSON.parse()` ao ler, conforme boas práticas do `localStorage`.

### Helper `DB` (main.js)

```js
const DB = {
    buscar: (chave) => JSON.parse(localStorage.getItem(chave)) || [],
    salvar: (chave, dado) => {
        try {
            const lista = DB.buscar(chave);
            lista.push(dado);
            localStorage.setItem(chave, JSON.stringify(lista));
            return true;
        } catch (e) {
            if (e.name === 'QuotaExceededError') {
                console.error('Limite de armazenamento atingido!');
            }
            return false;
        }
    }
};
```

---

## ▶️ Como Executar

1. Faça o download ou clone o repositório
2. Abra o arquivo `index.html` diretamente no navegador

> Nenhuma instalação, servidor ou dependência externa é necessária. O projeto roda 100% no frontend.

---

##  Páginas do Sistema

### Página Inicial
Menu de acesso rápido para as principais áreas do sistema.

### Cadastro de Filmes
Formulário completo com validação HTML5 nativa. Os filmes ficam disponíveis para seleção no cadastro de sessões.

### Cadastro de Salas
Registra salas com capacidade e tipo. A capacidade é usada para controle de lotação na listagem de sessões.

### Cadastro de Sessões
Carrega filmes e salas do `localStorage` dinamicamente nos campos `<select>`. Exibe lista das sessões cadastradas com opção de remoção.

### Listagem de Sessões
Exibe cards com todas as sessões disponíveis. Cada card mostra uma barra de progresso com ingressos vendidos vs. capacidade da sala. Sessões lotadas exibem o botão desabilitado automaticamente.

### Venda de Ingressos
Carrega sessões disponíveis no `<select>`. Suporta pré-seleção de sessão via parâmetro de URL (`?sessao=ID`), permitindo redirecionamento direto a partir da listagem.

---

##  Conceitos Aplicados

- Manipulação do DOM com JavaScript puro
- Criação dinâmica de elementos (`<option>` em `<select>`)
- Armazenamento e leitura de arrays de objetos com JSON
- Encadeamento de dados entre entidades (filme → sessão → ingresso)
- Navegação entre páginas via `<a href>`
- Passagem de parâmetros entre páginas via `URLSearchParams`
- Tratamento de erros com `try...catch` no `localStorage`

---

## 👨‍💻 Autor

Desenvolvido por **Arthur Cardoso das Dores**

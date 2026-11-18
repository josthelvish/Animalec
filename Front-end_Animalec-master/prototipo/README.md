# Animalec — Protótipo HTML5 do Back-office (Patrocinadores e Especialistas)

Projeto simplificado do Animalec que mostra, em HTML5 + Bootstrap 4, as views das duas novas entidades do Back-office:

- **Patrocinadores** (`SPONSORS` no código): um patrocinador pode patrocinar vários animais, e um animal pode ter vários patrocinadores, sem repetir o mesmo par.
- **Especialistas** (`EXPERTS` no código): cada especialista pertence a um grupo animal (anfíbio, ave, mamífero, peixe ou réptil) e é especialista de todos os animais desse grupo.

A interface está em português e o código usa os nomes em inglês do modelo de dados. Por ser um protótipo, gravar e remover só mostram um `alert`; nada é guardado.

## Como abrir

Basta abrir `index.html` num browser com ligação à Internet: Bootstrap, jQuery, Font Awesome e as fontes vêm de CDN. Não é preciso servidor nem instalação.

## Estrutura

```
prototipo/
├── index.html          Página de Administração (6 cartões; Patrocinadores e Especialistas ativos)
├── sponsors.html       Lista de patrocinadores (tabela em Web, cartões em Mobile, modal Ver, Remover)
├── sponsor_form.html   Adicionar / Editar patrocinador (?id=s01) + componente "Animais patrocinados"
├── experts.html        Lista de especialistas
├── expert_form.html    Adicionar / Editar especialista (?id=e01) + "Animais do grupo" (só leitura)
├── css/animalec.css    Tema do Animalec (cores #1abc9c / #2c3e50, Montserrat + Lato, divisor, chips, cartões)
├── img/                Logótipo, mascote e avatares dos animais (copiados de src/assets)
└── js/
    ├── data.js         Dados de exemplo (animais, patrocinadores, especialistas) e funções auxiliares
    ├── header.js       Cabeçalho comum (navbar) injetado em <header id="app-header">
    ├── footer.js       Rodapé comum injetado em <footer id="app-footer">
    ├── sponsors.js     Lógica das páginas de patrocinadores
    └── experts.js      Lógica das páginas de especialistas
```

## Modelo de dados usado (`js/data.js`)

| Entidade | Campos |
|---|---|
| Animal | `_id`, `name`, `group`, `avatar`, `sponsors: string[]` (ids de patrocinador, sem repetição) |
| Sponsor | `_id`, `name`, `type`, `description`, `contact {email, phone}`, `location {city, district, country}`, `links {logo, website}`, `sponsorship {start_date, end_date, amount}`, `active` |
| Expert | `_id`, `name`, `group`, `degree`, `institution`, `description`, `contact {email, phone}`, `location {city, district, country}`, `links {photo, website, orcid}`, `active` |

- Os animais de um patrocinador são `ANIMALS.filter(a => a.sponsors.includes(id))`.
- Os animais de um especialista são `ANIMALS.filter(a => a.group === expert.group)`.

## Semântica HTML5

- `<!DOCTYPE html>` e `lang="pt-PT"`; landmarks `<header>`, `<nav>`, `<main>` e `<footer>` em todas as páginas, e um link "Saltar para o conteúdo".
- Um só `<h1>` por página, dentro de `<section>` + `<header>`.
- Listas: `<table>` com `<caption>`, `<thead>`, `<th scope>` e `aria-sort`; em Mobile, um `<article>` por registo.
- Formulários: secções em `<fieldset>` + `<legend>`, `<label for>` em todos os campos, tipos `email`, `tel`, `url`, `date` e `number`, `required` e `pattern` (ORCID). A validação nativa do browser bloqueia a submissão.
- Pré-visualizações e miniaturas em `<figure>` + `<figcaption>`; detalhes no modal em `<dl>`.
- Links com aspeto de botão são `<a class="btn">`; nunca há um link dentro de um botão.

As 5 páginas passam no validador do W3C sem erros nem avisos. Ver `TESTES.md`.

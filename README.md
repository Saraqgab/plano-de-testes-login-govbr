# Plano de Testes — Tela de Login gov.br

## Objetivo

Este repositório documenta um exercício de **testes manuais de QA (Garantia de Qualidade)** aplicado à tela de login público do gov.br (`https://sso.acesso.gov.br`), com foco em validação de campos, tratamento de erros, acessibilidade e usabilidade.

O objetivo não é auditar ou explorar vulnerabilidades do sistema, e sim praticar e demonstrar competências de teste de interface web: elaboração de casos de teste, execução manual, documentação de bugs e análise de acessibilidade.

## Aviso importante

Todos os testes foram realizados de forma **manual e observacional**, sem uso de CPF ou senha reais, sem automação de requisições e **sem concluir nenhum login de fato**. O objetivo foi observar apenas o comportamento visual e as mensagens de validação exibidas pela interface.

## Escopo dos testes

- Validação de formato do campo CPF
- Validação do campo senha
- Comportamento com campos obrigatórios vazios
- Navegação por teclado (acessibilidade)
- Responsividade em diferentes tamanhos de tela
- Auditoria automatizada de acessibilidade (Google Lighthouse)

## Metodologia

- **Testes manuais de caixa-preta**: interação direta com a interface, sem conhecimento do código-fonte, apenas observando entradas e saídas.
- **Auditoria automatizada complementar**: uso do Google Lighthouse (DevTools do Chrome) para métricas objetivas de acessibilidade.

## Casos de teste

A lista completa de cenários testados, com passos, resultado esperado e resultado obtido, está no arquivo [`casos-de-teste.md`](./casos-de-teste.md).

## Principais achados

Os 10 casos de teste manuais não identificaram falhas de validação (todos passaram). No entanto, a auditoria automatizada de acessibilidade revelou problemas relevantes que não são visíveis durante um teste funcional comum, reforçando a importância de combinar testes manuais com ferramentas automatizadas.

### Bug 001 — Contraste de cores insuficiente
- **Severidade:** Média
- **Prioridade:** Média
- **Passos para reproduzir:** Observar o botão "bancos credenciados" e o selo de segurança no rodapé da tela de login
- **Resultado esperado:** Texto com contraste mínimo de 4.5:1 em relação ao fundo (conforme WCAG)
- **Resultado obtido:** 2 elementos identificados pelo Lighthouse com contraste insuficiente (texto verde `#008C32` sobre fundo claro)
- **Sugestão de correção:** Escurecer o tom de verde utilizado ou aumentar o peso da fonte nesses elementos

### Bug 002 — Imagens sem atributo `alt`
- **Severidade:** Média
- **Prioridade:** Alta
- **Passos para reproduzir:** Inspecionar os ícones da tela de login (ex: ícone de carteira de identidade, ícone de internet banking, ícone de QR code)
- **Resultado esperado:** Toda imagem informativa deve ter um texto alternativo descritivo (`alt="..."`), e imagens decorativas devem ter `alt=""`
- **Resultado obtido:** 6 imagens identificadas sem o atributo `alt`, prejudicando usuários de leitores de tela
- **Sugestão de correção:** Adicionar `alt` descritivo em cada ícone (ex: `alt="Ícone de identidade"`)

### Bug 003 — Links sem nome discernível
- **Severidade:** Alta
- **Prioridade:** Alta
- **Passos para reproduzir:** Navegar pela página usando um leitor de tela (ou inspecionar via DevTools) até o link de "alto contraste" e o link do VLibras
- **Resultado esperado:** Todo link deve ter um texto ou `aria-label` que descreva seu destino/função
- **Resultado obtido:** 2 links identificados sem nome acessível, aparecendo como "link vazio" para tecnologias assistivas
- **Sugestão de correção:** Adicionar `aria-label` descritivo, ex: `aria-label="Ativar modo de alto contraste"`

## Relatório de acessibilidade (Lighthouse)

Auditoria realizada com o Google Lighthouse (versão 13.4.1, motor de acessibilidade axe-core 4.12.1), em 05/09/2026, na tela `https://sso.acesso.gov.br/login`.

| Categoria | Pontuação |
|---|---|
| Acessibilidade | **73/100** |
| Boas Práticas | 54/100 |
| SEO | 82/100 |

**Principais pontos de melhoria identificados (Acessibilidade):**

1. **Contraste de cores insuficiente** em 2 elementos (detalhado no Bug 001)
2. **6 imagens sem atributo `alt`** (detalhado no Bug 002)
3. **2 links sem nome discernível** (detalhado no Bug 003)
4. **Zoom desabilitado no viewport** — a meta tag da página usa `maximum-scale=1.0` e `user-scalable=0`, o que impede usuários com baixa visão de ampliar a tela via gestos de pinça
5. **Link de "pular para o conteúdo" não está corretamente focável**, reduzindo sua utilidade para quem navega por teclado
6. **9 elementos com `tabindex` maior que 0**, o que quebra a ordem natural de navegação por Tab e pode confundir usuários de leitores de tela

**Observação sobre Boas Práticas e SEO:** embora fora do escopo principal deste teste (focado em acessibilidade), o Lighthouse também identificou o uso de APIs depreciadas, cookies de terceiros, erros registrados no console do navegador e ausência de meta description — pontos que podem ser citados como contexto adicional, mas não foram aprofundados neste relatório.

O relatório completo (HTML) está disponível na pasta [`evidencias/`](./evidencias).

## Evidências

Os prints de tela referentes a cada caso de teste estão organizados na pasta [`evidencias/`](./evidencias).

## Tecnologias e ferramentas utilizadas

- Testes manuais (exploração de interface)
- Google Chrome DevTools
- Google Lighthouse

## Sobre este projeto

Este repositório faz parte do meu portfólio de estudos em **Garantia de Qualidade (QA) e testes de interfaces web**, desenvolvido como prática complementar aos meus estudos em desenvolvimento front-end.

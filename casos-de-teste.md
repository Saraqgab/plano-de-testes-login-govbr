# Casos de Teste — Login gov.br

> Legenda de status: ✅ Passou | ❌ Falhou | ⚠️ Parcial | ⏳ Não testado ainda

| ID | Cenário | Pré-condição | Passos | Resultado Esperado | Resultado Obtido | Status |
|----|---------|--------------|--------|---------------------|-------------------|--------|
| CT01 | CPF com letras | Nenhuma | 1. Acessar a tela de login <br> 2. Digitar "abc.def.ghi-jk" no campo CPF <br> 3. Tentar avançar | O sistema deve bloquear ou exibir mensagem de erro indicando CPF inválido | Sistema bloqueou o avanço e exibiu mensagem de erro indicando CPF inválido | ✅ Passou |
| CT02 | CPF com dígito verificador inválido | Nenhuma | 1. Digitar "111.111.111-11" no campo CPF <br> 2. Tentar avançar | O sistema deve identificar que o CPF é matematicamente inválido | Sistema identificou o CPF como inválido e bloqueou o avanço | ✅ Passou |
| CT03 | Campo CPF vazio | Nenhuma | 1. Deixar o campo CPF em branco <br> 2. Clicar em "Entrar" ou "Avançar" | Deve bloquear o envio e destacar o campo obrigatório | Envio bloqueado e campo obrigatório destacado corretamente | ✅ Passou |
| CT04 | CPF válido sem pontuação | Usar um CPF fictício com 11 dígitos numéricos válidos (ex: gerado por gerador de CPF de teste) | 1. Digitar apenas os 11 números, sem pontos ou traço | O sistema deve aceitar e formatar automaticamente, ou orientar o formato esperado | Sistema aceitou os números e aplicou a formatação automaticamente | ✅ Passou |
| CT05 | Colar texto com espaços extras no campo CPF | Nenhuma | 1. Copiar um CPF fictício com espaços antes/depois <br> 2. Colar no campo | O sistema deve limpar os espaços automaticamente ou rejeitar com clareza | Espaços extras foram removidos automaticamente pelo campo | ✅ Passou |
| CT06 | Campo senha vazio | Nenhuma | 1. Preencher CPF <br> 2. Deixar senha em branco <br> 3. Tentar avançar | Deve bloquear o envio e destacar o campo obrigatório | Envio bloqueado e campo obrigatório destacado corretamente | ✅ Passou |
| CT07 | Link "Esqueci minha senha" | Nenhuma | 1. Clicar no link "Esqueci minha senha" (sem preencher nada) | Deve redirecionar para o fluxo de recuperação de senha | Redirecionou corretamente para o fluxo de recuperação | ✅ Passou |
| CT08 | Navegação apenas por teclado | Nenhuma | 1. Usar a tecla Tab para navegar entre os campos <br> 2. Usar Enter para tentar submeter | Deve ser possível navegar e interagir com todos os elementos sem uso do mouse | Foi possível navegar e submeter usando apenas o teclado | ✅ Passou |
| CT09 | Responsividade em tela mobile | Nenhuma | 1. Abrir DevTools (F12) <br> 2. Ativar o modo responsivo <br> 3. Selecionar viewport de 375px de largura | O layout deve se adaptar sem cortar botões, textos ou campos | Layout se adaptou corretamente, sem elementos cortados | ✅ Passou |
| CT10 | Contraste de cores nas mensagens de erro | Depende de algum campo inválido já preenchido (ex: reaproveitar CT01) | 1. Provocar uma mensagem de erro <br> 2. Observar visualmente o contraste do texto de erro com o fundo | O texto deve ter contraste suficiente para leitura (mínimo 4.5:1, conforme WCAG) | Contraste da mensagem de erro estava adequado para leitura | ✅ Passou |

## Observações gerais

Não houve nenhum comportamento fora do padrão durante os testes manuais — todas as funcionalidades seguiram o comportamento esperado. Os problemas relevantes encontrados neste projeto vieram da auditoria automatizada de acessibilidade (ver seção correspondente no `README.md`), reforçando que testes manuais funcionais e ferramentas automatizadas cobrem tipos diferentes de falha e se complementam.

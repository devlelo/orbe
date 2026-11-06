# Orbe

Aplicação de gestão simples para pequenos negócios, desenvolvida primeiro como PWA mobile-first. Não usa menu lateral: a dashboard apresenta quatro ações principais e cada área tem uma seta para regressar ao início.

## Áreas principais

- **Vender:** pesquisa de produtos, carrinho, cliente opcional, método de pagamento e confirmação de venda paga. A entrega é definida por produto.
- **Produtos:** nome, categoria, custo unitário, preço de venda, stock inicial e mínimo; editar e remover produtos.
- **Stock:** entradas, saídas manuais, correções e histórico de movimentos.
- **Clientes:** cadastro opcional e histórico de compras.

## Dashboard e ferramentas secundárias

- Total vendido hoje, lucro estimado, número de produtos e alertas de stock.
- Vendas recentes e produtos que precisam de reposição.
- Histórico de vendas, relatórios, registo de despesas e definições.
- Exportação CSV, impressão/guardar como PDF e backup/restauro JSON.

## Persistência e instalação

- SQLite executado com sql.js/WebAssembly.
- Base de dados guardada no armazenamento local do navegador (IndexedDB).
- Primeira abertura: escolher armazenamento local ou uma pasta num computador cujo navegador suporte File System Access API.
- Quando configurada, a pasta mantém uma cópia do ficheiro `orbe.sqlite`; no telemóvel, usa-se o armazenamento privado da aplicação.
- PWA com cache do shell e runtime SQLite para utilização offline depois da primeira abertura e cache inicial.
- Sem conta e sem sincronização automática entre dispositivos.

## Executar localmente

Servir esta pasta por HTTP/HTTPS (service workers não funcionam em `file://`):
```bash
python -m http.server 8080
```
Abrir http://localhost:8080.

## Limitações ainda por resolver

- A seleção de pasta não é suportada em todos os navegadores móveis.
- A primeira inicialização precisa carregar o runtime SQLite.
- CSV não é XLSX nativo; PDF é feito através da impressão do navegador.
- Ainda não inclui caixa completo, dívidas/pagamentos parciais, calculadora de custos integrada, fotos de produtos ou gestão de encomendas.
- Não é faturação certificada nem integração AGT.

## Testes obrigatórios antes de usar comercialmente

1. Criar produto e editar o stock.
2. Registar venda paga, verificar baixa de stock e lucro.
3. Tentar adicionar mais unidades do que o stock disponível.
4. Registar venda com e sem cliente.
5. Alterar entrega de cada produto individualmente.
6. Reabrir a aplicação e verificar persistência.
7. Exportar e restaurar backup.
8. Instalar PWA e testar offline.
9. Num computador compatível, testar a cópia SQLite na pasta escolhida.

MIT License.
# Orbeo Gestão

Aplicação web progressiva (PWA) para gestão simples de pequenos negócios. Interface em português, mobile-first, sem menu lateral complexo e preparada para funcionar offline depois da primeira inicialização.

## Módulos atuais

- **Dashboard:** vendas do dia, lucro estimado, produtos, stock baixo e dívidas.
- **Vendas:** carrinho, seleção de cliente, método de pagamento, pagamento total ou parcial e criação automática de dívida quando existe saldo por receber.
- **Produtos:** catálogo com fotografia, preço de custo, preço de venda, quantidade, stock mínimo e cálculo rápido do lucro por unidade.
- **Calculadora de custos:** escolhe primeiro um produto; divide custo de caixa por unidades ou soma compra, transporte e outros custos. Sugere preços e permite aplicar custo e preço à ficha do produto.
- **Stock:** entradas, correções, alertas e histórico de movimentos.
- **Clientes:** cadastro e histórico de compras.
- **Dívidas:** registo manual ou criado por venda parcialmente paga, recebimentos parciais e histórico de pagamentos.
- **Encomendas:** cliente, descrição, valor total, recebido, data prevista e estado.
- **Despesas:** registo de gastos por categoria.
- **Histórico e relatórios:** consulta de vendas, exportação CSV e impressão/guardar em PDF.
- **Ajustes:** moeda, nome do negócio e backup/restauro.

## Regras funcionais

- O custo e o preço de cada venda ficam registados como fotografia histórica; alterações posteriores ao produto não reescrevem vendas antigas.
- O lucro realizado é calculado a partir das vendas registadas, e não do stock ainda por vender.
- Uma venda parcialmente paga exige cliente identificado e gera automaticamente uma dívida pelo valor em falta.
- A calculadora é independente, mas só calcula depois de o utilizador escolher um produto.
- O resultado da calculadora só atualiza a ficha do produto após confirmação.
- O utilizador pode cadastrar produtos manualmente ou sem informar custo.
- Fotografias de produtos são guardadas localmente como dados da aplicação.

## Base de dados e armazenamento

- SQLite executado no navegador através de SQLite/WebAssembly (sql.js).
- O ficheiro SQLite é persistido no armazenamento privado do navegador (IndexedDB).
- Na primeira abertura, o utilizador escolhe guardar neste dispositivo ou, em navegadores de computador compatíveis, selecionar uma pasta para manter também o ficheiro `orbe.sqlite`.
- A seleção de pastas depende da File System Access API, disponível sobretudo em navegadores Chromium de computador. Em telemóveis e navegadores sem essa API, os dados ficam no armazenamento privado da aplicação.
- O runtime SQLite é colocado em cache pelo service worker para permitir aberturas seguintes sem ligação, depois da primeira inicialização.
- Os dados são locais ao dispositivo; não existe sincronização automática entre telefone e computador.
- Backup e restauro transportam produtos, vendas, clientes, stock, dívidas, pagamentos, encomendas, despesas e configurações.

## Executar localmente

Sirva esta pasta por HTTP/HTTPS (service workers não funcionam em `file://`). Por exemplo:

```bash
python -m http.server 8080
```

Abra http://localhost:8080.

## Próximas etapas

1. Testes manuais de todos os fluxos e validação dos cálculos.
2. Melhorias de UX e correções identificadas nos testes.
3. Rever a estratégia SQLite no Android com Capacitor e plugin SQLite nativo.
4. Preparar build Android e automatização do APK com GitHub Actions.

## Limitações conhecidas

- A escolha de pasta não é suportada por todos os navegadores; no telemóvel, usa-se o armazenamento privado do navegador.
- É necessário acesso à internet na primeira inicialização para carregar o runtime SQLite, caso ainda não esteja em cache.
- CSV abre no Excel, mas não é um ficheiro XLSX nativo.
- PDF é gerado pela impressão do navegador; escolha “Guardar como PDF”.
- Não é software de faturação fiscal certificado e não faz integração AGT.

## Testes manuais prioritários

1. Criar produto com preço manual, só preço de venda e modo de cálculo.
2. Carregar fotografia e confirmar que permanece após recarregar.
3. Calcular custo de caixa dividido por unidades e aplicar ao produto.
4. Fazer venda integral e confirmar decremento de stock.
5. Fazer venda parcial com cliente e confirmar criação da dívida.
6. Registar pagamento parcial e total da dívida.
7. Criar encomenda, atualizar estado e registar despesa.
8. Recarregar e confirmar persistência SQLite.
9. Instalar PWA e abrir offline depois da primeira inicialização.
10. Exportar e restaurar backup num dispositivo de teste.

## Licença

MIT. Ver LICENSE.

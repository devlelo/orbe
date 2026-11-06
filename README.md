# Orbe

Aplicação de gestão simples para pequenos negócios. Interface mobile-first, sem menu lateral e com quatro áreas principais: Vender, Produtos, Stock e Clientes.

## Experiência
- Dashboard com vendas de hoje, lucro estimado, catálogo e alertas de stock.
- Cada área abre numa tela própria com seta de regresso.
- Vendas com cliente opcional, pagamento integral e estado de entrega por produto.
- Produtos com custo, preço, categoria, quantidade e stock mínimo.
- Stock com entradas, saídas e correções com histórico de movimentos.
- Clientes com histórico de compras.
- Histórico, relatórios, CSV, impressão/PDF e backup/restauro JSON.

## Dados
- SQLite via sql.js/WebAssembly.
- Base de dados persistida localmente em IndexedDB, sem conta e sem sincronização cloud.
- No primeiro acesso, escolha entre armazenamento local e pasta no computador compatível; a pasta recebe uma cópia `orbe.sqlite`.
- A seleção de pasta depende da File System Access API; não está disponível em todos os telemóveis/navegadores.
- O runtime SQLite é colocado em cache pelo service worker para aberturas posteriores offline, depois da primeira inicialização.

## Executar
Servir por HTTP/HTTPS, nunca por `file://`:
```bash
python -m http.server 8080
```

## Limitações
- A pasta é uma cópia local no navegador compatível, não é sincronização entre dispositivos.
- A primeira abertura precisa carregar o runtime SQLite.
- CSV não é XLSX nativo; PDF usa a impressão do navegador.
- Não é faturação certificada nem integração AGT.

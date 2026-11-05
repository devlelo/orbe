# Orbe

Aplicação web progressiva (PWA) para gestão simples de pequenos negócios. Interface em português, mobile-first, sem menu lateral.

## Quatro funções principais

- **Vender:** carrinho simples, pagamento integral e cliente opcional.
- **Produtos:** catálogo, custo, preço de venda e stock inicial.
- **Stock:** entradas, correções, alertas de reposição e movimentos.
- **Clientes:** contactos e histórico de compras.

A dashboard apresenta total vendido hoje, lucro estimado, quantidade de produtos e alertas de stock baixo. Cada área abre numa tela própria com seta para regressar ao início.

## Base de dados e armazenamento

- SQLite executado no navegador através de SQLite/WebAssembly (sql.js).
- O ficheiro SQLite é persistido no armazenamento privado do navegador (IndexedDB).
- Na primeira abertura, o utilizador escolhe guardar neste dispositivo ou, em navegadores de computador compatíveis, selecionar uma pasta para manter também o ficheiro `orbe.sqlite`.
- A seleção de pastas depende da File System Access API, disponível sobretudo em navegadores Chromium de computador. Em telemóveis e navegadores sem essa API, os dados ficam no armazenamento privado da aplicação.
- O runtime SQLite é colocado em cache pelo service worker para permitir aberturas seguintes sem ligação, depois da primeira inicialização.
- Os dados são locais ao dispositivo; não existe sincronização automática entre telefone e computador.

## Executar localmente

Sirva esta pasta por HTTP/HTTPS (service workers não funcionam em `file://`). Por exemplo:

```bash
python -m http.server 8080
```

Abra http://localhost:8080.

## Limitações conhecidas

- A escolha de pasta não é suportada por todos os navegadores; no telemóvel, usa-se o armazenamento privado do navegador.
- É necessário acesso à internet na primeira inicialização para carregar o runtime SQLite, caso ainda não esteja em cache.
- CSV abre no Excel, mas não é um ficheiro XLSX nativo.
- PDF é gerado pela impressão do navegador; escolha “Guardar como PDF”.
- Não é software de faturação fiscal certificado e não faz integração AGT.

## Testes manuais prioritários

1. Criar produto e conferir quantidade inicial.
2. Fazer venda paga e confirmar decremento de stock.
3. Tentar vender acima do stock e confirmar bloqueio.
4. Fazer venda sem cliente e com cliente.
5. Alterar o estado de entrega por item na venda.
6. Recarregar e confirmar persistência SQLite.
7. Instalar PWA e abrir offline depois da primeira inicialização.
8. Confirmar criação e atualização de `orbe.sqlite` numa pasta escolhida em computador compatível.

## Licença

MIT. Ver LICENSE.

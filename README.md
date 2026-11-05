# Orbe

Aplicação web progressiva (PWA) para gestão simples de pequenos negócios. Interface em português, mobile-first e armazenamento local.

## Funcionalidades da primeira versão

- Cadastro e edição de produtos, custo, preço, stock e mínimo.
- Registo de vendas com pagamento integral obrigatório.
- Cliente opcional; histórico de compras quando identificado.
- Estado de entrega independente do pagamento, por item vendido.
- Atualização automática do stock e histórico de movimentos.
- Painel diário, lucro estimado, alertas de stock.
- Exportação de vendas CSV (compatível com Excel), relatório imprimível/Guardar como PDF e backup/restauro JSON.
- IndexedDB como armazenamento local principal (requer um navegador moderno com suporte a IndexedDB).
- PWA com cache dos ficheiros essenciais para abrir offline depois da primeira visita.

## Executar localmente

Sirva esta pasta por HTTP/HTTPS (service workers não funcionam em file://). Por exemplo:

```bash
python -m http.server 8080
```

Abra http://localhost:8080.

## Limitações conhecidas desta versão

- Os dados são locais ao navegador e dispositivo; não há sincronização automática entre telefone e computador.
- O acesso a uma pasta do dispositivo depende do navegador e da autorização do utilizador; backup manual está disponível em navegadores modernos.
- CSV abre no Excel, mas ainda não é um ficheiro XLSX nativo.
- O PDF é gerado pela função de impressão do navegador; escolha “Guardar como PDF”.
- Não é software de faturação fiscal certificado e não faz integração AGT.

## Testes manuais prioritários

1. Criar produto e conferir quantidade inicial.
2. Fazer venda paga e confirmar decremento de stock.
3. Tentar vender acima do stock e confirmar bloqueio.
4. Fazer venda sem cliente e com cliente.
5. Alterar estado de entrega por produto.
6. Recarregar e confirmar persistência.
7. Instalar PWA, abrir offline e navegar.
8. Exportar CSV, imprimir PDF e restaurar backup.

## Licença

MIT. Ver LICENSE.
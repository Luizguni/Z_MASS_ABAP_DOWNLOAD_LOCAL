
# Z_MASS_ABAP_DOWNLOAD_LOCAL

## Visão Geral

O programa `Z_MASS_ABAP_DOWNLOAD_LOCAL` foi desenvolvido para facilitar a exportação em massa de objetos ABAP customizados (com prefixo `Z*`) diretamente para o ambiente local do usuário. Ele oferece suporte para exportar programas (`REPO`), funções (`FUGR`, `FUNC`) e enhancements (includes de enhancement). Além disso, gera logs detalhados e organiza os arquivos de forma estruturada por tipo de objeto.

---

## Funcionalidades

- Exportação de programas do tipo:
  - Reports (`Z*`)
  - Funções (`FUNCTION-GROUP`, `FUNCTION-MODULE`)
  - Enhancements (`ENHO`, `ENHS`)
- Download local direto do SAP GUI
- Seleção de pasta local para armazenamento
- Geração de log de execução no formato `.txt`
- Classe de exportação orientada a objetos (`lcl_exportador_programas`)
- Código comentado conforme boas práticas ABAP
- Testes unitários incluídos com `ABAP Unit`

---

## Estrutura do Projeto

```
Z_MASS_ABAP_DOWNLOAD_LOCAL/
├── src/
│   ├── main.abap                # Programa principal
│   ├── classes/
│   │   └── lcl_exportador_programas.abap
│   └── includes/
│       └── z_log_writer.abap
├── tests/
│   └── test_lcl_exportador.abap
├── logs/
│   └── export_log_YYYYMMDD.txt
└── README.md
```

---

## Como Executar

1. Acesse a SE38 ou SE80 no SAP.
2. Execute o programa `Z_MASS_ABAP_DOWNLOAD_LOCAL`.
3. Selecione o tipo de objeto desejado (report, função ou enhancement).
4. Informe a pasta de destino local (pop-up via `GUI_FILE_SAVE_DIALOG`).
5. Execute (F8).
6. Verifique o log gerado na mesma pasta do download.

---

## Classe Principal

**Classe:** `lcl_exportador_programas`  
**Responsabilidade:** Gerenciar a lógica de leitura de repositório, filtragem por tipo e prefixo `Z`, extração dos fontes e gravação dos arquivos no diretório local escolhido pelo usuário.

---

## Testes Unitários

Testes foram desenvolvidos para validar os principais métodos da classe exportadora, utilizando `FOR TESTING` e `CLASS lcl_test DEFINITION`.

---

## Pré-requisitos

- SAP GUI com permissões de leitura de objetos no repositório (`REPOSRC`, `TFDIR`, `ENLFDIR`, etc.)
- Permissão para execução de programas customizados
- Acesso à pasta local pelo SAP GUI

---

## Exemplo de Uso

```abap
PARAMETERS: p_progr  TYPE c RADIOBUTTON GROUP g01,
            p_funcao TYPE c RADIOBUTTON GROUP g01,
            p_enhanc TYPE c RADIOBUTTON GROUP g01.

PARAMETERS: pfolder TYPE localfile.

START-OF-SELECTION.

  DATA(lo_exportador) = NEW lcl_exportador_programas( ).
  lo_exportador->exportar( tipo = 'PROGRAMA' diretorio = pfolder ).
```

---

## Logs de Exportação

Cada execução gera um log com os seguintes dados:
- Data/hora da exportação
- Objetos exportados
- Sucessos e falhas
- Caminho de destino

Formato: `export_log_YYYYMMDD.txt`

---

## Licença

Este projeto é distribuído sob licença livre para fins de estudo e melhoria contínua em ambientes SAP internos.

---

## Autor

**Guni**  
Desenvolvedor ABAP & Java  
[LinkedIn](https://www.linkedin.com) | [GitHub](https://github.com)

---

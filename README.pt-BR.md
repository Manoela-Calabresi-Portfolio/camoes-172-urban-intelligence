# Camões 172 · inteligência territorial aplicada

Versão em português-BR do projeto **Camões 172 — Urban Intelligence Pipeline**.

## O que este caso é

Sistema geoespacial de ponta a ponta para apoiar decisões de localização, produto e posicionamento urbano. O projeto integra dados territoriais, mercado imobiliário e regras urbanas em uma mesma estrutura analítica, organizada para virar WebGIS e dossiê de decisão.

## Pergunta central

Como transformar dados urbanos, regulatórios, censitários e de mercado em uma leitura territorial consistente para apoiar decisões imobiliárias e urbanas em um caso real.

## O que este caso mostra

- integração real entre censo, território e mercado;
- base analítica em PostGIS para leitura urbana;
- transformação de dados em WebGIS e dossiê para cliente;
- uso de IBGE/SIDRA como parte do sistema, não como caso isolado.

## Visão do sistema

![Visão geral do sistema Camões 172](assets/camoes-system-overview.svg)

## Bases integradas

- GeoCuritiba / ArcGIS REST;
- IBGE SIDRA API;
- OpenStreetMap;
- LiDAR;
- listings de mercado.

## Coleta de dados

O caso não parte de uma única base. Ele consolida fluxos diferentes de coleta e atualização:

| Fonte | Como entra | O que alimenta |
|---|---|---|
| GeoCuritiba / ArcGIS REST | download estruturado por camadas e serviços municipais | cadastro, zoneamento, transporte e contexto urbano |
| IBGE / SIDRA | consulta por API e seleção de tabelas | renda, domicílio, escolaridade e leitura censitária |
| OpenStreetMap | extração por Overpass e processamento espacial | rede, POIs, edificações e suporte à acessibilidade |
| LiDAR | ingestão de DSM/DTM | modelagem de alturas e morfologia |
| Mercado | coleta de listings e snapshots mensais | preço, oferta, tipologia e leitura de produto |

Em termos práticos, o sistema coleta:

- dados regulatórios e cadastrais;
- infraestrutura e rede urbana;
- dados censitários;
- dados físicos do tecido construído;
- dados dinâmicos de mercado.

## Fluxo do sistema

```mermaid
flowchart LR
    A[Dados territoriais e de mercado] --> B[PostGIS]
    B --> C[Camadas analíticas]
    C --> D[WebGIS]
    C --> E[Dossiê]
    C --> F[Decisão locacional e produto]
```

## 1. Banco espacial

O banco separa ingestão, referência, análise e motor paramétrico de zoneamento em esquemas distintos. Isso permite atualizar mercado, geometrias e visões analíticas sem confundir funções ou corromper histórico.

![Estrutura do banco e normalização de zoneamento](https://github.com/user-attachments/assets/cc7cadad-9dac-464c-91fd-e01854626077)

O que este bloco entrega:

- organização robusta em PostGIS;
- separação entre dados frios, dinâmicos e derivados;
- base para regras de zoneamento e leitura analítica.

## 2. Engenharia de pipeline

O sistema opera com lógica HOT/COLD. Listings entram por pipeline próprio, com contrato de snapshot e UPSERT; camadas geoespaciais entram por reposição controlada, com dependências explicitamente recriadas.

![Fluxo de pipeline e coleta](https://github.com/user-attachments/assets/083472a4-7c8e-4f90-afcd-cd45ad0bbb0e)

### Fluxos coletados

**Fluxo 1 · Territorial público**

- coleta de camadas municipais;
- normalização espacial;
- persistência em banco para cruzamentos regulatórios e urbanos.

**Fluxo 2 · Censitário**

- busca e seleção de tabelas no SIDRA;
- integração de variáveis censitárias;
- uso como base para indicadores territoriais.

**Fluxo 3 · OSM**

- extração de rede, POIs e edificações;
- organização em camadas reutilizáveis;
- apoio a leitura de acessibilidade e contexto urbano.

**Fluxo 4 · LiDAR**

- entrada de superfícies e elevação;
- derivação de alturas e intensidade construída;
- suporte a leitura morfológica.

**Fluxo 5 · Mercado**

- coleta de listings por snapshot;
- histórico consistente com UPSERT;
- base para leitura de preço, oferta e produto.

O que este bloco entrega:

- atualização confiável de dados de mercado;
- separação entre coleta e reprocessamento;
- pipeline repetível para novos ciclos de análise.

## 3. Integração geoespacial

O caso combina fontes heterogêneas com formatos, CRS e periodicidades diferentes. Tudo entra em CRS padronizado e passa a conversar em uma mesma base espacial.

![Integração entre fontes geoespaciais](https://github.com/user-attachments/assets/072d0853-b4a2-42ee-a79d-e10ef5477599)

Fontes que entram aqui:

- cadastro e zoneamento municipais;
- IBGE/SIDRA para renda, domicílio e escolaridade;
- OSM para rede, POIs e edificações;
- LiDAR para modelagem de alturas;
- mercado para leitura de preço, oferta e produto.

## 4. WebGIS e entrega ao cliente

O resultado não fica só no banco. As camadas analíticas viram visualizador navegável e dossiê editorial para leitura do caso.

### Recortes de mapa

#### Mapa de demanda

![Mapa de demanda](assets/mapa_s6_demanda.png)

#### Mapa de submercado

![Mapa de submercado](assets/mapa_s6_submercado.png)

Esses recortes mostram o tipo de leitura que o WebGIS permite:

- demanda territorial;
- submercados;
- relações entre produto, estrutura urbana e contexto regulatório.

![WebGIS Camões 172 · vista 1](https://github.com/user-attachments/assets/d6c2b30b-e13e-4df0-a25b-7050e2ca1ddb)

![WebGIS Camões 172 · vista 2](https://github.com/user-attachments/assets/7ffeb968-a2c2-421e-8934-3c9ed6aee835)

![WebGIS Camões 172 · vista 3](https://github.com/user-attachments/assets/0287e1f6-3ab9-4c2e-aaa5-77f9952dba4e)

### Ênfase no WebGIS

O WebGIS não é uma camada decorativa. Ele é a superfície de trabalho entre análise e apresentação:

- organiza a leitura espacial em sequências comparáveis;
- permite navegar entre demanda, submercado, morfologia, envelope regulatório e mercado;
- traduz visões do banco em mapas utilizáveis por cliente e equipe;
- mantém a mesma lógica de navegação em novos estudos.

O que este bloco entrega:

- leitura navegável do território;
- passagem direta de análise para apresentação;
- reutilização da mesma estrutura em novos estudos.

## 5. Inteligência urbana e imobiliária

O caso transforma o território em decisão. A camada analítica avalia cenários de produto, submercado, envelope regulatório, concentração econômica e tensões frente ao mercado.

![Tabela de cenários e ranking](https://github.com/user-attachments/assets/14c8f5b0-43a9-48e7-92e0-1e37d22c360f)

O que este bloco entrega:

- leitura comparável entre território, regulação e mercado;
- avaliação de cenários de produto;
- apoio a localização e desenvolvimento imobiliário.

## Resultado final

- sistema replicável de inteligência territorial;
- integração entre censo, mercado e geografia urbana;
- apoio a avaliação de localização, produto e desenvolvimento;
- entrega técnica e editorial no mesmo fluxo.

## Ferramentas

Python · PostGIS · GeoPandas · MapLibre GL JS · GeoParquet · IBGE SIDRA API · GeoCuritiba · OSM · LiDAR

## Ver arquivos do projeto

[Abrir repositório completo](https://github.com/Manoela-Calabresi-Portfolio/camoes-172-urban-intelligence)

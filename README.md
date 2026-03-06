# Detecção Automática de Telhados para AutoCAD

Este projeto é uma **prova de conceito (PoC)** que explora o uso de **visão computacional com Python** para identificar telhados em imagens de satélite e gerar automaticamente marcações utilizáveis no AutoCAD.

A ideia é reduzir drasticamente o trabalho manual de identificar e marcar casas em projetos urbanos.

## Como funciona

A partir de uma imagem de satélite, o sistema utiliza técnicas de **OpenCV** para detectar regiões que correspondem a telhados.

Essas regiões são convertidas em **polígonos vetoriais**, e o centro geométrico de cada telhado é identificado.

O resultado é exportado como um **arquivo DXF**, contendo:

- o contorno de cada telhado detectado
- uma marcação com a letra **"C"** posicionada no centro de cada área

Esse arquivo pode então ser aberto diretamente no **AutoCAD**, permitindo integrar o resultado ao fluxo de trabalho existente.

## Objetivo

O objetivo principal desta prova de conceito é validar um fluxo automatizado:

Imagem de satélite → Detecção de telhados → Vetorização → Exportação DXF → Uso no AutoCAD

Caso validado, o projeto poderá evoluir para uma ferramenta mais completa de automação para projetos urbanos.

# INSTRUCTIONS.md

Objetivo

Este documento descreve como usar a Proof of Concept para detectar telhados em imagens aéreas e gerar arquivos DXF.


Pré-requisitos

Python instalado.

Dependências listadas em requirements.txt.


Instalação

Instalar dependências com:

pip install -r requirements.txt


Estrutura esperada do projeto

O projeto deve conter os seguintes diretórios principais:

samples
output


Adicionar imagens de teste

Colocar imagens de telhados dentro da pasta:

samples/


Executar o projeto

Executar o arquivo principal:

python main.py


Fluxo de execução

Quando executado, o programa irá:

1 carregar a imagem definida no main.py
2 detectar o contorno principal do telhado
3 simplificar esse contorno em um polígono
4 exportar o resultado como um arquivo DXF


Resultado esperado

Após a execução, um arquivo DXF será gerado dentro da pasta:

output/

Esse arquivo pode ser aberto em softwares CAD.


Sobre as imagens

Para melhores resultados:

- usar imagens aéreas
- visão ortogonal (top-down)
- telhados bem visíveis
- pouco ruído visual


Limitações da PoC

Esta versão:

- não usa inteligência artificial
- assume um telhado principal por imagem
- pode falhar em casos de vegetação ou sombras fortes


Objetivo desta versão

O objetivo desta PoC é validar o pipeline completo:

imagem -> detecção -> polígono -> DXF


Melhorias futuras

Possíveis evoluções incluem:

- detecção de múltiplos telhados
- melhoria da simplificação geométrica
- alinhamento automático de ângulos
- uso de modelos de segmentação com IA
- extração de dimensões reais


Uso pretendido

Este projeto é voltado para experimentação, prototipagem e validação de ideias antes da construção de uma solução mais robusta.
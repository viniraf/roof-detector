# ARCHITECTURE.md

Objetivo do projeto

Este projeto é uma Proof of Concept para detectar automaticamente o contorno de telhados em imagens aéreas e exportar esse contorno como um arquivo DXF que pode ser utilizado em softwares CAD.

A arquitetura é propositalmente simples para facilitar:

- entendimento do código
- experimentação
- iteração rápida
- uso de ferramentas de IA como Copilot e Cursor


Pipeline do sistema

O fluxo completo do sistema é:

1 carregar imagem
2 detectar contorno do telhado
3 simplificar contorno para polígono
4 exportar polígono para DXF


Estrutura de arquivos

main.py  
detector.py  
utils.py  
dxf.py  
samples/  
output/  
requirements.txt  
README.md  


Responsabilidade de cada arquivo


main.py

Arquivo de entrada do programa.

Responsável por:

- carregar a imagem
- chamar o detector
- simplificar o polígono
- exportar o resultado em DXF

O main.py deve ser curto e apenas orquestrar o pipeline.


detector.py

Contém o algoritmo de detecção do telhado.

Responsável por:

- pré-processamento da imagem
- detecção de bordas
- detecção de contornos
- seleção do contorno principal

Entrada:

imagem OpenCV

Saída:

lista de pontos representando o contorno do telhado


utils.py

Funções auxiliares de geometria e utilidades.

Exemplos:

- simplify_polygon
- order_points
- largest_contour
- centroid
- debug helpers

Esse arquivo evita que detector.py fique muito grande.


dxf.py

Responsável pela exportação do polígono para DXF.

Entrada:

lista de pontos do polígono

Saída:

arquivo DXF salvo no diretório output


samples/

Contém imagens de teste usadas durante desenvolvimento.

Essas imagens são utilizadas para validar o algoritmo.


output/

Diretório onde arquivos gerados são salvos.

Exemplos:

roof.dxf
debug_edges.png
debug_contours.png


Design principles

A arquitetura segue alguns princípios simples:

- poucos arquivos
- funções pequenas
- responsabilidades claras
- fácil leitura
- fácil modificação


Sem uso de classes inicialmente

Para a PoC evitamos estruturas complexas.

Preferimos funções puras como:

detect_roof(image)

simplify_polygon(contour)

export_dxf(points, path)

Isso torna o código mais simples para leitura e também mais fácil para ferramentas de IA entenderem o contexto.


Fluxo de dados

imagem -> detector -> contorno -> simplificação -> polígono -> exportação DXF


Critério de sucesso da arquitetura

A arquitetura deve permitir que qualquer pessoa consiga entender o fluxo do projeto rapidamente apenas lendo o main.py.
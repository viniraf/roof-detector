Projeto: Roof Detector PoC

Objetivo da PoC
Detectar automaticamente telhados em imagens de satélite e gerar um arquivo DXF contendo polígonos dos telhados e o texto "C" no centro.

Escopo da PoC
- detectar um telhado dominante na imagem
- gerar polígono aproximado
- calcular centroide
- exportar DXF

Fora do escopo
- múltiplos telhados complexos
- machine learning
- georreferenciamento

Fase 1 - Estrutura do projeto
Criar arquivos base e funções vazias.

Arquivos:
utils.py
detector.py
dxf.py
main.py

DoD
Projeto roda sem erro.

--------------------------------------------------

Fase 2 - Pipeline de visão computacional

Implementar:
- preprocessamento
- detecção de bordas
- fechamento morfológico
- detecção de contornos

DoD
Imagem gera contorno detectado.

--------------------------------------------------

Fase 3 - Vetorização

Implementar:
- simplificação de polígono
- cálculo de centroide

DoD
Contorno vira polígono válido.

--------------------------------------------------

Fase 4 - Exportação DXF

Implementar:
- criação de polylines
- inserção do texto "C"

DoD
Arquivo DXF gerado corretamente.

--------------------------------------------------

Fase 5 - Execução completa

Pipeline:

imagem → detector → polígono → centroide → DXF

DoD
Rodar:

python main.py

gera um DXF válido.
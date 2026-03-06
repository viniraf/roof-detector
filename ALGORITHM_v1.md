Objetivo

Detectar automaticamente o contorno principal de um telhado em imagens aéreas (ortofotos) e converter esse contorno em um polígono simplificado que posteriormente será exportado como DXF.

Este algoritmo é uma abordagem clássica baseada em visão computacional (OpenCV), sem uso de IA. A meta da PoC é atingir aproximadamente 80–90% de precisão em telhados simples e bem contrastados em ortofotos.

O algoritmo assume:

- Imagem aérea vista de cima
- Telhado ocupando parte significativa da imagem
- Bordas relativamente bem definidas
- Pouca oclusão por árvores


Pipeline geral

1. Carregar imagem
2. Pré-processar imagem
3. Detectar bordas
4. Detectar contornos
5. Selecionar contorno principal
6. Simplificar contorno para polígono
7. Ordenar pontos do polígono
8. Retornar polígono final


Etapa 1 — Carregamento da imagem

A imagem deve ser carregada usando OpenCV.

Requisitos:
- imagem colorida
- resolução razoável
- formato PNG ou JPG

Exemplo lógico:

image = cv2.imread(path)


Etapa 2 — Pré-processamento

Converter para escala de cinza para simplificar o processamento.

gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

Aplicar blur leve para remover ruído de textura.

blur = cv2.GaussianBlur(gray, (5,5), 0)

Esse passo ajuda a melhorar a detecção de bordas.


Etapa 3 — Detecção de bordas

Usar Canny Edge Detection.

edges = cv2.Canny(
    blur,
    threshold1=50,
    threshold2=150
)

Isso cria um mapa de bordas da imagem.


Etapa 4 — Reforço das bordas

Para fechar pequenos buracos nas bordas:

kernel = np.ones((3,3), np.uint8)

edges = cv2.dilate(edges, kernel, iterations=1)
edges = cv2.erode(edges, kernel, iterations=1)

Esse processo ajuda a criar contornos mais contínuos.


Etapa 5 — Detecção de contornos

Detectar contornos usando OpenCV:

contours, _ = cv2.findContours(
    edges,
    cv2.RETR_EXTERNAL,
    cv2.CHAIN_APPROX_SIMPLE
)

Usamos RETR_EXTERNAL para ignorar contornos internos.


Etapa 6 — Selecionar o contorno principal

Selecionar o maior contorno pela área.

largest = max(contours, key=cv2.contourArea)

Filtrar contornos muito pequenos caso necessário.

if cv2.contourArea(contour) < MIN_AREA:
    ignorar

Isso evita detectar carros, sombras ou ruído.


Etapa 7 — Simplificação do contorno

Usar algoritmo Douglas-Peucker para simplificar.

epsilon = 0.02 * cv2.arcLength(contour, True)

polygon = cv2.approxPolyDP(
    contour,
    epsilon,
    True
)

Isso transforma o contorno em um polígono com poucos vértices.


Etapa 8 — Converter para lista de pontos

Extrair pontos do polígono.

points = [(x, y) for [[x,y]] in polygon]


Etapa 9 — Ordenar os pontos

Ordenar pontos em ordem consistente (sentido horário).

Isso evita problemas ao exportar para DXF.

Estratégia simples:

1. Calcular centroide
2. Ordenar por ângulo polar


Etapa 10 — Retorno final

Retornar lista de pontos:

[(x1,y1),
 (x2,y2),
 (x3,y3),
 (x4,y4),
 ...]

Esses pontos serão usados para gerar o DXF.


Possíveis melhorias futuras

- filtrar contornos por retangularidade
- detectar múltiplos telhados
- ignorar vegetação usando cor
- usar Hough lines para reforçar arestas
- snapping de ângulos para 90 graus
- usar segmentação com IA


Resultado esperado da PoC

Entrada:
imagem aérea simples contendo uma casa.

Saída:
polígono aproximado do telhado principal.

O polígono deve representar corretamente:

- orientação do telhado
- número aproximado de lados
- proporções do telhado


Critério de sucesso da PoC

O algoritmo deve conseguir detectar corretamente o telhado principal na maioria das imagens simples sem ajustes manuais.
# Benchmarking de Modelos YOLO-Seg para Detecção de EPIs

Este repositório contém o código para benchmark de diferentes versões e precisões de modelos YOLO de segmentação (YOLO-Seg) para detecção de Equipamentos de Proteção Individual (EPIs). O objetivo é avaliar o desempenho (mAP, latência e uso de memória) de modelos como YOLOv8 e possivelmente outros (YOLOv11, YOLOv26) em diferentes tamanhos (nano, small, medium, large) e precisões (FP32, FP16, INT8).

## Sumário do Projeto

O projeto foca na avaliação comparativa de modelos YOLO-Seg para identificar a combinação mais eficiente (modelo, tamanho, precisão) para detecção de EPIs. Isso envolve:

1.  **Configuração do Ambiente:** Instalação de dependências e montagem do Google Drive para armazenamento.
2.  **Preparação do Dataset:** Download de um dataset de EPIs (via Roboflow), balanceamento e divisão em conjuntos de treino, validação e teste.
3.  **Treinamento:** Treinamento de modelos YOLO-Seg com diferentes configurações.
4.  **Avaliação:** Medição de métricas de desempenho, latência e uso de memória (VRAM/RAM) para cada modelo e precisão.
5.  **Geração de Relatórios:** Consolidação dos resultados em um DataFrame e exportação para CSV.

## Estrutura do Repositório (Notebook Colab)

O projeto é implementado em um notebook Google Colab, que guia através das seguintes etapas:

-   **Célula 1: Configuração do Ambiente e Download do Dataset:** Instalação de bibliotecas (`ultralytics`, `roboflow`, `grad-cam`, `tensorrt`), montagem do Google Drive e download do dataset de EPIs via Roboflow.
-   **Célula 2: Balanceamento e Divisão do Dataset:** Scripts para rebalancear e dividir o dataset em proporções adequadas para treino, validação e teste, garantindo a reprodutibilidade.
-   **Célula 3: Configurações de Treinamento e Funções de Monitoramento:** Definição de parâmetros de treinamento (versões, tamanhos, precisões) e uma função para monitorar o uso de memória (VRAM e RAM) durante a inferência.
-   **Célula 4: Treinamento dos Modelos Ultralytics:** Loop principal para treinar os modelos YOLO-Seg, salvando os pesos treinados no Google Drive.
-   **Célula 5: Avaliação e Benchmark de Modelos por Precisão:** Avaliação dos modelos treinados em diferentes precisões (FP32, FP16, INT8), medindo mAP, latência e uso de memória. Os resultados são compilados e salvos em um arquivo CSV.

## Pré-requisitos

Para executar este notebook, você precisará de:

-   Uma conta Google para usar o Google Colab.
-   Acesso ao Google Drive para salvar os pesos e resultados dos modelos.
-   Uma chave de API Roboflow (já configurada no notebook, mas você pode usar a sua).

## Como Usar

1.  **Abrir no Google Colab:** Clique no botão "Open in Colab" (se disponível) ou faça o upload do notebook para o seu ambiente Colab.
2.  **Configurar Roboflow API Key:** Certifique-se de que sua chave de API Roboflow esteja configurada (atualmente, ela está diretamente no código da Célula 1).
3.  **Montar Google Drive:** Execute a Célula 1 para montar seu Google Drive. Isso é crucial para salvar os pesos do modelo e evitar perdas ao final da sessão do Colab.
4.  **Executar as Células:** Execute as células sequencialmente. O notebook é projetado para ser executado de cima para baixo.
5.  **Acompanhar o Treinamento e Avaliação:** Monitore os outputs das células para acompanhar o progresso do treinamento e da avaliação.
6.  **Verificar Resultados:** Ao final da execução da Célula 5, um arquivo `resultados_benchmark_segmentacao_oficial.csv` será salvo no seu Google Drive, contendo o benchmark completo.

## Resultados Esperados

O arquivo CSV final (`resultados_benchmark_segmentacao_oficial.csv`) conterá as seguintes métricas para cada modelo (versão, tamanho) e precisão testada:

-   **Modelo:** e.g., `YOLOV8-SEG`
-   **Tamanho:** e.g., `N` (nano), `S` (small), `M` (medium), `L` (large)
-   **Precisão:** e.g., `FP32`, `FP16`, `INT8`
-   **mAP50_Box:** Mean Average Precision @ 0.5 IoU para caixas delimitadoras.
-   **mAP50_Mask:** Mean Average Precision @ 0.5 IoU para máscaras de segmentação.
-   **mAP50-95_Mask:** Mean Average Precision @ 0.5-0.95 IoU para máscaras de segmentação.
-   **Latencia_ms:** Tempo médio de inferência em milissegundos.
-   **VRAM_Pico_MB:** Pico de uso de VRAM em MB durante a inferência.
-   **VRAM_Media_MB:** Uso médio de VRAM em MB durante a inferência.
-   **RAM_Media_MB:** Uso médio de RAM em MB durante a inferência.

Estes resultados permitirão uma análise detalhada da trade-off entre precisão, velocidade e consumo de recursos para diferentes configurações de modelos de detecção de EPIs.

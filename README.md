
# Segmentação de Barbas Masculinas

## Introdução

Este projeto faz parte da unidade curricular de Aprendizagem Profunda para Visão por Computador, integrada no Mestrado em Ciência de Dados. O objetivo é desenvolver modelos eficazes para a segmentação de barbas em imagens de rostos masculinos, abordando os desafios impostos pela variabilidade nas formas, tamanhos e estilos de barba.

A segmentação precisa de barbas tem implicações práticas notáveis, como a melhoria de sistemas de reconhecimento facial e a aplicação em contextos de segurança.

## Descrição Geral do Sistema

### Abordagens Utilizadas

Para este projeto, utilizámos duas abordagens distintas com o modelo de segmentação SAM desenvolvido pela Meta:

1. **Primeira Abordagem:**
   - Utilização de imagens obtidas aleatoriamente da internet.
   - Aplicação da função `SamAutomaticMaskGenerator(sam)` para criar máscaras de segmentação Zero Shot.
   - Conversão e redimensionamento das imagens para 1024x1024 pixels.
   - Utilização do `MaskAnnotator` para sobrepor máscaras e destacar áreas segmentadas.
   - Conclusão: Esta abordagem foi descartada devido ao tempo excessivo de processamento e dificuldades na segmentação de barbas curtas.

2. **Segunda Abordagem:**
   - Utilização de três estratégias distintas com datasets diferentes.
   - Organização de ficheiros com imagens, anotações e um ficheiro CSV para o dataset completo.
   - Criação de arrays numpy com coordenadas das caixas delimitadoras.
   - Definição de preditores de máscaras utilizando `SamPredictor(sam)`.

### Datasets

Foram utilizados três datasets:

1. [Beard Detection by Ridzeuss](https://universe.roboflow.com/ridzeuss/bearddetection)
2. [Beard Dataset by Naved Qureshi](https://universe.roboflow.com/naved-qureshi/beard-dataset)
3. [AIFaceAttribute Dataset](https://universe.roboflow.com/aifaceattribute/aifaceattribute)

O dataset final foi construído organizando as imagens e máscaras em diretórios específicos para treino e validação, com uma divisão de 80% para treino e 20% para validação.

## Modelos de Segmentação

### Primeira Estratégia

- Utilização do modelo ResNet50-UNet com 256 classes e dimensões de entrada de 224x224 pixels.
- Treinamento do modelo durante 20 épocas com `EarlyStopping`.
- Teste do modelo com imagens aleatórias do dataset e avaliação das métricas de desempenho.

### Segunda Estratégia

- Definição dos diretórios de treino e validação.
- Utilização da classe `ImageDataGenerator` do TensorFlow para normalizar os dados.
- Implementação de uma classe `DisplayPredictions` para monitorizar o desempenho do modelo durante o treino.
- Construção e compilação de uma U-Net, utilizando a perda de Dice e o coeficiente de Dice como métricas.
- Treino do modelo com `model.fit` e utilização de callbacks para monitorização do desempenho.

## Resultados

Os resultados foram avaliados com base em métricas de precisão, acurácia, recall e F1 score.

- **FCN-8s VGG:** Acurácia de 25,5%, precisão de 65,7%.
- **MobileNet SegNet:** Acurácia de 77,4%, precisão de 81,2%.
- **MobileNet U-Net:** Acurácia de 88,9%, F1 score de 80,1%.
- **PSPNet:** Pior desempenho com acurácia de 21,1%, F1 score de 26,2%.
- **U-Net:** Acurácia de 70,2%, precisão de 75,5%.
- **VGG SegNet:** Acurácia de 79,0%, F1 score de 59,8%.

## Conclusões

- A primeira abordagem foi ineficaz devido ao tempo de processamento e dificuldade na segmentação de barbas curtas.
- A segunda abordagem demonstrou a importância da escolha adequada do modelo e da qualidade dos datasets.
- O modelo MobileNet U-Net foi o mais eficiente.
- Melhorias futuras poderiam incluir aumento da variedade e número de imagens no dataset, utilização de técnicas de augmentation e uso de imagens de maior resolução.

## Referências Bibliográficas

1. Roboflow (2024). Beard Detection by Ridzeuss. Disponível em: [https://universe.roboflow.com/ridzeuss/bearddetection](https://universe.roboflow.com/ridzeuss/bearddetection)
2. Roboflow (2024). Beard Dataset by Naved Qureshi. Disponível em: [https://universe.roboflow.com/naved-qureshi/beard-dataset](https://universe.roboflow.com/naved-qureshi/beard-dataset)
3. Roboflow (2024). AiFaceAttribute Dataset. Disponível em: [https://universe.roboflow.com/aifaceattribute/aifaceattribute](https://universe.roboflow.com/aifaceattribute/aifaceattribute)
4. Stack Overflow (2024). Keras Image Segmentation using Grayscale Masks and ImageDataGenerator Class. Disponível em: [https://stackoverflow.com/questions/53248099/keras-image-segmentation-using-grayscale-masks-and-imagedatagenerator-class](https://stackoverflow.com/questions/53248099/keras-image-segmentation-using-grayscale-masks-and-imagedatagenerator-class)


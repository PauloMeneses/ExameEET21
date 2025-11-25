# 🎧 Classificação de Áudios do UrbanSound8K usando GMM e HMM

## 🎓 Instituto Tecnológico de Aeronáutica (ITA)  
### Disciplina: **EET21 — Processamento Digital de Sinais**  
### Professores:
- Prof. **Bartolomeu Ferreira Uchoa Filho**  
- Profa. **Sarah Negreiros de Carvalho Leite**

---

# 📌 Autores
- **Paulo Vitor Meneses Andrade**  
- **Gabriel Rocha**

Este repositório contém os códigos, experimentos e resultados produzidos para o Exame Final da disciplina *Processamento Digital de Sinais*, aplicando técnicas de classificação de áudio ao dataset **UrbanSound8K**.

---

# 📦 Dataset

Dataset oficial contendo 8732 áudios classificados em 10 classes sonoras:

📎 **Link oficial:**  
https://www.kaggle.com/datasets/chrisfilo/urbansound8k

O arquivo de metadados `UrbanSound8K.csv` foi incluído neste repositório.

---

# 🧪 Metodologia

A pipeline inclui:

### 🔊 1. Extração de Características
- **Dufaux Transient Detection** (energia por quadro, mediana, contagem de transientes)  
- **MFCC + Delta + Delta²** (médias)  
- **Mel-Spectrogram** (estatísticas)

As features finais concatenam:

```
[dufaux_stats] + [mel_mean] + [mfcc_mean + delta_mean + delta2_mean]
```

---

### 🔁 2. Validação Cruzada (10 folds)
Usamos os folds originais do UrbanSound8K:

- Treina GMM em 9 folds e testa no fold restante  
- Treina HMM por classe usando sequências MFCC+Delta  
- Salva métricas, predições e matrizes de confusão  

---

### 🤖 3. Classificadores utilizados

#### **GMM**
- 8 componentes  
- Covariância diagonal  
- PCA opcional (40 componentes)  
- Predição por maior verossimilhança

#### **HMM**
- 3 estados ocultos  
- Emissão gaussiana  
- Treinamento por classe usando sequências temporais  

---

# 📁 Estrutura do Repositório

```
ExameEET/
│
├── UrbanSound8K.csv
│
├── classweights.ipynb
├── eetexame.ipynb
├── plotResults.ipynb
│
├── results/
│   ├── gmm_preds_foldX.npy
│   ├── hmm_preds_foldX.npy
│   ├── gmm_fold_accuracy.npy
│   ├── hmm_fold_accuracy.npy
│   ├── summary.json
│   └── figs/
│       ├── class_distribution_urbansound8k.png
│       ├── 02_acuracia_media.png
│       ├── 03_boxplot.png
│       ├── 04_confusion_matrix_gmm.png
│       └── 05_confusion_matrix_hmm.png
│
└── results.zip
```

---

# 📊 Resultados

Os resultados estão na pasta `results/`, contendo:

- Acurácia por fold  
- Acurácia média  
- Boxplot dos folds  
- Matrizes de confusão normalizadas  
- Figuras exportadas automaticamente  

O arquivo `summary.json` contém todas as métricas finais.

---

# ▶️ Como Reproduzir

### **1. Baixe e extraia o UrbanSound8K**

Estrutura esperada:

```
fold1/
fold2/
...
fold10/
UrbanSound8K.csv
```

### **2. Ajuste o caminho base**

No arquivo `pipeline_main.py`:

```python
base_path = r"E:\ExameEET"
```

### **3. Execute a pipeline**

```bash
python eetexame.ipynb
```

### **4. Gere as figuras**

Execute:

```
plotResults.ipynb
```

---

# 📝 Histórico de Commits

### **1) Add Database Metadata file**
Inserção do arquivo `UrbanSound8K.csv`.

### **2) Add classweights.ipynb**
Notebook de análise da distribuição das classes.

### **3) Add pipeline code**
Pipeline completa com:
- Dufaux  
- MFCC  
- Mel  
- PCA  
- GMM/HMM  
- 10-fold cross-validation  
- Salvamento de resultados  

### **4) Add output file (zip)**
Notebook exportado como ZIP.

### **5) Add notebook that makes and saves result images**
Geração automática dos gráficos.

### **6) Add all results (unpacked) and images**
Inclusão de imagens e resultados finais.

---

# 🏁 Conclusões

- O pipeline reproduz e compara duas técnicas probabilísticas clássicas aplicadas a áudio.  
- A análise combina características temporais e espectrais.  
- Resultados organizados para replicação e visualização.  

---

# 📦 Requirements

Para instalar todas as dependências:

```bash
pip install -r requirements.txt
```

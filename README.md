# Projeto-YouTube-Pipeline

# Projeto YouTube Pipeline
**Versão:** 1.6 – Atualizado em 26/10/2025  
**Autores:** Danilo Ye, Daniel Zou, Igor Shirata Duarte  
**Instituição:** Universidade Presbiteriana Mackenzie – FCI  

---

## Descrição
Pipeline automatizado para mineração multimodal de vídeos de **unboxing no YouTube**, com foco em **inteligência de mercado** aplicada ao **varejo de importação**.

O sistema integra **coleta, transcrição, NLP e análise de tópicos**, gerando indicadores como **sentimento médio**, **palavras-chave predominantes** e **temas emergentes** por canal ou marca.

---

## Estrutura Geral

---

## ⚙️ Módulos Principais

### 🔹 1. Coleta de Dados
| Script | Função | Saída |
|--------|---------|-------|
| `yt_collect_videos.py` | Coleta metadados de vídeos via **YouTube Data API v3** | `videos.csv` |
| `yt_collect_comments.py` | Coleta comentários dos vídeos (autor, data, texto) | `comments.csv` |

---

### 🔹 2. Pré-processamento e Filtragem
| Script | Função | Saída |
|--------|---------|-------|
| `step_eda.py` | Realiza **análise exploratória de dados (EDA)** e limpeza de colunas | `videos_clean.csv` |
| `step_filter.py` | Aplica filtros de duração ≥60s, idioma e duplicidade | `videos_clean_filtered.csv` |

---

### 🔹 3. Transcrição (ASR)
| Script | Função | Saída |
|--------|---------|-------|
| `asr_whisper.py` | Transcreve áudios com **OpenAI Whisper (small/base)** | `transcripts.csv` |
| `check_transcripts.py` | Verifica falhas ou trechos não transcritos | logs e mensagens no terminal |

---

### 🔹 4. Análise de Linguagem Natural (NLP)
| Script | Função | Saída |
|--------|---------|-------|
| `nlp_stage.py` | Executa **KeyBERT** e **XLM-RoBERTa** para sentimento | `dataset_nlp.csv` |
| `comments_sentiment.py` | Classifica sentimentos dos comentários do público | `comments_sentiment.csv` |
| `brand_entity_extract.py` | Detecta marcas e entidades mencionadas (NER) | `dataset_brands.csv` |

---

### 🔹 5. Agrupamento de Tópicos
| Script | Função | Saída |
|--------|---------|-------|
| `topics_bertopic.py` | Identifica padrões temáticos com **BERTopic** | `dataset_topics.csv` |
| `topics_overview.csv` | Relatório sintético dos tópicos detectados | `topics_overview.csv` |

---

### 🔹 6. Consolidação e BI
| Script | Função | Saída |
|--------|---------|-------|
| `make_aggregates.py` | Gera agregações (sentimento médio, volume) | `agg_channel.csv`, `agg_brand.csv` |
| `exports_bi.py` | Cria tabelas fato e dimensão para Power BI | `bi_fato_videos.csv`, `bi_agg_channel.csv` |

---

### 🔹 7. Automação e Controle
| Arquivo | Função |
|----------|---------|
| `run_all.bat` | Executa o pipeline completo sequencialmente |
| `requirements.txt` | Lista todas as dependências (`pip install -r requirements.txt`) |

---

## 🔁 Fluxo Geral do Pipeline

```mermaid
graph TD
A[yt_collect_videos.py] --> B[step_eda.py]
B --> C[step_filter.py]
C --> D[asr_whisper.py]
D --> E[nlp_stage.py]
E --> F[topics_bertopic.py]
F --> G[make_aggregates.py]
G --> H[exports_bi.py]
H --> I[Power BI Dashboard]

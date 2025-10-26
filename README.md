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


## ⚙️ Descrição dos Módulos Principais

### 🔹 1. Coleta de Dados
| Script | Descrição | Saída |
|--------|------------|-------|
| `yt_collect_videos.py` | Coleta metadados (título, canal, views, likes) via YouTube Data API v3 | `videos.csv` |
| `yt_collect_comments.py` | Coleta comentários, autores e datas dos vídeos | `comments.csv` |

---

### 🔹 2. Pré-processamento e Filtragem
| Script | Descrição | Saída |
|--------|------------|-------|
| `step_eda.py` | Limpeza e análise exploratória (EDA) | `videos_clean.csv` |
| `step_filter.py` | Filtragem por idioma, duração e duplicatas | `videos_clean_filtered.csv` |

---

### 🔹 3. Transcrição (ASR)
| Script | Descrição | Saída |
|--------|------------|-------|
| `asr_whisper.py` | Transcreve áudio com OpenAI Whisper (small/base) | `transcripts.csv` |
| `check_transcripts.py` | Verifica falhas ou vazios na transcrição | Logs no terminal |

---

### 🔹 4. NLP e Análise Semântica
| Script | Descrição | Saída |
|--------|------------|-------|
| `nlp_stage.py` | Extração de palavras-chave (KeyBERT) e sentimento (XLM-RoBERTa) | `dataset_nlp.csv` |
| `comments_sentiment.py` | Classificação de sentimento dos comentários | `comments_sentiment.csv` |
| `brand_entity_extract.py` | Detecção de marcas e entidades nomeadas (NER) | `dataset_brands.csv` |

---

### 🔹 5. Agrupamento de Tópicos
| Script | Descrição | Saída |
|--------|------------|-------|
| `topics_bertopic.py` | Agrupamento temático com BERTopic (multilíngue) | `dataset_topics.csv` |
| `topics_overview.csv` | Resumo dos tópicos e clusters gerados | `topics_overview.csv` |

---

### 🔹 6. Consolidação e Business Intelligence
| Script | Descrição | Saída |
|--------|------------|-------|
| `make_aggregates.py` | Calcula médias de sentimento por canal/marca | `agg_channel.csv` |
| `exports_bi.py` | Cria tabelas fato e dimensão para Power BI | `bi_fato_videos.csv`, `bi_agg_channel.csv`, `bi_agg_brand.csv` |

---

### 🔹 7. Automação e Execução
| Arquivo | Descrição |
|----------|-----------|
| `run_all.bat` | Executa o pipeline completo sequencialmente e gera logs |
| `requirements.txt` | Lista todas as dependências para instalação via `pip` |

---

## 🔁 Fluxo Lógico do Pipeline

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

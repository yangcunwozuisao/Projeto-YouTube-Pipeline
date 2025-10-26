# Projeto-YouTube-Pipeline

# 🎥 Projeto YouTube Pipeline
**Versão:** 1.6 – Atualizado em 26/10/2025  
**Autores:** Danilo Ye, Daniel Zou, Igor Shirata Duarte  
**Instituição:** Universidade Presbiteriana Mackenzie – FCI  

---

## 📖 Descrição
Pipeline automatizado para mineração multimodal de vídeos de **unboxing no YouTube**, com foco em **inteligência de mercado** aplicada ao **varejo de importação**.

O sistema integra **coleta, transcrição, NLP e análise de tópicos**, gerando indicadores como **sentimento médio**, **palavras-chave predominantes** e **temas emergentes** por canal ou marca.

---

## ⚙️ Estrutura Geral
projeto_youtube_pipeline/
│
├── .venv/                         # Ambiente virtual Python
├── data/                          # Diretório opcional para armazenar datasets e áudios
│
├── agg_channel.csv                # Agregação de métricas por canal
├── bi_agg_brand.csv               # Tabela BI com agregados por marca
├── bi_agg_channel.csv             # Tabela BI com agregados por canal
├── bi_fato_videos.csv             # Tabela fato consolidada (Power BI)
│
├── brand_entity_extract.py        # Script de extração de entidades (marcas, produtos)
├── check_transcripts.py           # Validação de transcrições ASR
├── comments_sentiment.py          # Análise de sentimento em comentários
├── comments.csv                   # Base original de comentários do YouTube
│
├── dataset_brands.csv             # Base de dados de entidades nomeadas (marcas)
├── dataset_nlp_plus.csv           # Dataset NLP expandido (keywords + sentimento + tópicos)
├── dataset_nlp.csv                # Dataset NLP principal (texto e sentimento)
├── dataset_topics.csv             # Tópicos detectados pelo BERTopic
│
├── exports_bi.py                  # Gera arquivos para Power BI (fato e dimensões)
├── make_aggregates.py             # Gera agregações de sentimento por canal/marca
│
├── nlp_stage.py                   # Extração de keywords e análise de sentimento (KeyBERT + XLM-R)
├── requirements.txt               # Dependências do projeto
│
├── step_eda.py                    # Limpeza e análise exploratória inicial (EDA)
├── step_filter.py                 # Filtros de duração, idioma e qualidade de vídeo
│
├── topics_bertopic.py             # Agrupamento temático (BERTopic)
├── topics_overview.csv            # Resumo dos tópicos encontrados
│
├── transcripts.csv                # Transcrições geradas pelo Whisper
├── videos_clean_filtered.csv      # Base limpa e filtrada (pós-EDA)
├── videos_clean.csv               # Base limpa de metadados
├── videos_top50.csv               # Subamostra de vídeos para teste
├── videos.csv                     # Base original coletada pela API
│
├── yt_collect_comments.py         # Coleta de comentários via YouTube Data API
├── yt_collect_videos.py           # Coleta de metadados de vídeos via YouTube Data API
│
└── run_all.bat                    # Script de automação e execução completa do pipeline


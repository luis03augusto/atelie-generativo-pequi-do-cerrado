# 🎨 Ateliê Generativo Rupestre

## 📜 Sobre o Projeto
Este repositório contém o projeto prático de pós-graduação focado no desenvolvimento e implantação de um **pipeline multimodal de Inteligência Artificial Generativa**. 

A aplicação interativa recebe uma ideia curta do usuário, expande conceitualmente esse texto utilizando um LLM, gera uma pintura estilizada baseada em Arte Rupestre através de um modelo de difusão ajustado (Fine-Tuning com LoRA) e, simultaneamente, narra a descrição da cena através de um modelo de síntese de voz (TTS).

## ⚙️ Arquitetura do Sistema
O pipeline foi estruturado de forma modular e sequencial, processado em GPU (CUDA) com gestão explícita de memória, integrando os seguintes modelos fundacionais:
* **Expansão de Texto (LLM):** `Qwen/Qwen2.5-0.5B-Instruct`
* **Geração de Imagem:** `stable-diffusion-v1-5/stable-diffusion-v1-5` + LoRA Customizado (`LuisCurado/lora-estilo-rupestre`)
* **Síntese de Voz (TTS):** `suno/bark-small`
* **Interface Web:** Gradio

## 📂 Estrutura do Repositório
O desenvolvimento foi dividido em quatro etapas documentadas nos seguintes cadernos de execução:

* 📄 `01_dataset.ipynb`: Script de processamento de dados. Realiza o *auto-captioning* (legendagem automática) de um banco de imagens utilizando o modelo **BLIP**, injetando o *trigger word* `estilo_rupestre,` e exportando os metadados no formato `metadata.jsonl`.
* 📄 `02_treino_lora.ipynb`: Rotina de ajuste fino (*Fine-Tuning*) do Stable Diffusion v1.5. Utiliza a biblioteca `accelerate` e a técnica *Low-Rank Adaptation* (LoRA) para ensinar o estilo rústico e abstrato ao modelo base (precisão `fp16`, otimização `cosine`).
* 📄 `03_avaliacao.ipynb`: Avaliação técnica do modelo. Contém a geração de grades comparativas visuais (Base vs. LoRA), testes de memorização (overfitting) e o cálculo quantitativo de fidelidade texto-imagem utilizando a métrica matemática **CLIPScore**.
* 📄 `app.ipynb`: Código-fonte da aplicação final. Consolida o frontend em Gradio e o fluxo de dados entre os três modelos de inferência, com tratamento de exceções e túnel reverso para acesso web.

## 📊 Resultados e Avaliação
A aplicação bem-sucedida do LoRA forçou a rede neural a abandonar sua tendência ao fotorrealismo padrão, adaptando os tensores para replicar o desgaste, as silhuetas irregulares e a textura rochosa exigidas pelo domínio ancestral. A métrica CLIPScore confirmou a consistência semântica entre os prompts instruídos e as saídas abstratas geradas.

## ⚖️ Reflexão Ética
O projeto inclui uma análise sobre o impacto do uso de IA generativa em patrimônios culturais. A conversão de arte rupestre ancestral em dados sintéticos levanta debates sobre apropriação, propriedade intelectual de povos originários e o risco de desinformação arqueológica, exigindo transparência clara na interface sobre a natureza sintética das imagens.

## 👨‍💻 Autor
**Luis Curado**
* [\[Link para o LinkedIn\]](https://www.linkedin.com/in/luis-curado-478539a2/)
* [\[Link para o Portfólio/Hugging Face\]](https://huggingface.co/LuisCurado)
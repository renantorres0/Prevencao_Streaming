# Prevenção Streaming - Modelo de Previsão de Churn

## 📌 Visão Geral do Projeto

Este projeto tem como objetivo desenvolver um modelo preditivo para identificar clientes com alta probabilidade de cancelamento (churn) em uma plataforma de streaming. Através de técnicas de machine learning e análise exploratória, buscamos fornecer insights valiosos para estratégias de retenção de clientes.

## 🛠️ Ferramentas Utilizadas

- **Linguagens**: Python, SQL
- **Bibliotecas**: 
  - SciKit Learn (Regressão Logística, Random Forest, GridSearchCV)
  - Python Graph Gallery (visualização)
  - Pandas, NumPy (manipulação de dados)
- **Ambiente**: Google Colab
- **Visualização**: Matplotlib, Seaborn

## 📊 Estrutura dos Dados

O conjunto de dados original contém as seguintes variáveis:

| Coluna | Descrição | Tipo | Observações |
|--------|-----------|------|-------------|
| client_id | Identificador único do cliente | Int | Chave primária |
| age | Idade do cliente | Int | Valores entre 18-80 |
| gender | Gênero do cliente | String | M/F/Outro |
| region | Região geográfica | String | 5 regiões distintas |
| subscription_days | Tempo como assinante | Int | Em dias corridos |
| subscription_type | Tipo de plano | String | Basic/Standard/Premium |
| num_contents | Conteúdos assistidos | Int | Últimos 30 dias |
| avg_rating | Avaliação média dada | Float | Escala 1-5 |
| num_active_profiles | Perfis ativos | Int | 1-5 perfis |
| num_streaming_services | Serviços concorrentes | Int | Quantidade total |
| devices_connected | Dispositivos ativos | Int | 1-10 dispositivos |
| churned | Indicador de cancelamento | Int | 0=Não, 1=Sim |

## 🔍 Análise Exploratória (EDA)

Principais descobertas:

![Distribuição de Churn por Idade](https://github.com/user-attachments/assets/0a7800e7-b911-436d-bb22-939510f5bbc8)
*Figura 1: Relação entre idade e taxa de churn*

![Correlação entre Variáveis](https://github.com/user-attachments/assets/8a25f7f0-6510-4014-a7e9-279d967a2fcb)

*Figura 2: Matriz de correlação entre features*

Principais insights:
- Clientes com mais de 60 dias de assinatura têm 40% menos churn
- Usuários que avaliam conteúdos abaixo de 2.5 têm 3x mais churn
- Plano Premium apresenta 25% menos cancelamentos

## 🧹 Pré-processamento de Dados

Etapas realizadas:
1. **Tratamento de missing values**:
   - Preenchimento de avg_rating com mediana por tipo de plano
   - Exclusão de 5 registros com dados críticos faltantes

2. **Engenharia de features**:
   - Criação de `content_per_day = num_contents/subscription_days`
   - Binning de idade em categorias (18-25, 26-35, etc.)
   - One-hot encoding para variáveis categóricas

3. **Balanceamento**:
   - Aplicação de SMOTE para equilibrar classes (churn 15% original)

## 🤖 Modelagem Preditiva

### 1. Regressão Logística (Baseline)

![Resultados Regressão Logística](https://github.com/user-attachments/assets/b32766e9-d573-486a-b6fc-5cb70b59963d)

*Figura 3: Métricas do modelo inicial*

- Acurácia: 78%
- Recall: 72% (critério principal para negócio)
- Features mais importantes: subscription_days, avg_rating, num_streaming_services

### 2. Otimização com GridSearch

![Tuning de Hiperparâmetros](https://github.com/user-attachments/assets/21428ec5-eaf4-4784-81b3-9b0a1869ab31)

*Figura 4: Curva de validação para parâmetro C*

Melhorias obtidas:
- Aumento de 5% no recall
- Redução de overfitting (diferença train-test de 15% para 8%)

### 3. Random Forest (Modelo Final)

![Importância de Features](https://github.com/user-attachments/assets/01dc7263-9d8b-4b6f-be8c-bebe70bdd8e9)

*Figura 5: Features mais relevantes no modelo final*

Métricas finais:
- **Acurácia**: 84%
- **Recall**: 82% 
- **Precisão**: 79%
- **AUC-ROC**: 0.89

## 🚀 Como Reproduzir

1. Clone o repositório:
   ```bash
   git clone https://github.com/renantorres0/Prevencao_Streaming.git
   ```

2. Execute o notebook
   
## 📈 Próximos Passos

- [ ] Implementar API para predições em tempo real
- [ ] Testar modelos com dados de novos mercados
- [ ] Desenvolver dashboard de monitoramento contínuo
- [ ] Adicionar análise de sentimentos de reviews

## 🤝 Contribuição

Contribuições são bem-vindas! Siga estes passos:
1. Abra uma issue descrevendo sua sugestão
2. Faça um fork do projeto
3. Crie um branch para sua feature (`git checkout -b feature/AmazingFeature`)
4. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
5. Push para o branch (`git push origin feature/AmazingFeature`)
6. Abra um Pull Request

## ✉️ Contato

Renan Torres - [nantorres0@gmail.com]

# 🚀 Desafio Técnico: Performance Test - BlazeDemo

Este repositório contém a automação de testes de performance para o cenário de compra de passagens aéreas no site [BlazeDemo](https://www.blazedemo.com). O objetivo é validar a estabilidade e o tempo de resposta do sistema sob uma carga específica.

---

## 🛠️ Tecnologias Utilizadas
* **Apache JMeter 5.x**
* **Java 11+**
* **HTML Dashboard Report** 

---

## 🚀 Como Executar o Script
1. Clone este repositório:
```bash
git clone git@github.com:GabiGomess/AgibankPerformance.git
```
2. Execute o teste com o seguinte comando:
```bash
jmeter -n -t ./scripts/script.jmx -l ./results/log_execucao.jtl -e -o ./results/dashboard -f
```

## 📊 Relatório de Execução (CI/CD)
Os testes são executados automaticamente via GitHub Actions. O relatório histórico e detalhado do Allure Report pode ser visualizado online através do link abaixo:

👉 [Acesse o Relatório de Testes Aqui](https://gabigomess.github.io/AgibankPerformance/)

---

## 📋 Cenário de Teste
Simulação do fluxo de compra ponta a ponta:
1.  **Home:** Acesso à página inicial.
2.  **Reserva:** Seleção de cidades de origem e destino.
3.  **Escolha de Voo:** Seleção da companhia aérea e preço.
4.  **Compra:** Preenchimento dos dados do passageiro.
5.  **Confirmação:** Validação da mensagem de sucesso ("Thank you for your purchase today!").

## 📈 Critérios de Aceitação
De acordo com os requisitos técnicos:
* **Vazão Alvo:** 250 requisições por segundo (RPS).
* **Performance:** 90th Percentile (P90) inferior a **2 segundos**.

---

## 📊 Relatório de Execução e Conclusão
### Resumo dos Resultados
| Métrica | Valor Obtido | Status |
|---------|--------------|--------|
| Throughput Médio | 46,4 req/s | ❌ NOK |
| 90th Percentile (P90) | 7224ms | ❌ NOK |
| Taxa de Erro | 0.00% | ✅ OK |

---

## 🚨 Conclusão Técnica
O critério de aceitação para este cenário de performance NÃO foi satisfeito. Abaixo, detalho a análise técnica comparando os requisitos com os valores obtidos:

1. **Análise de Vazão (Throughput)**
**Critério Exigido**: 250 requisições por segundo (RPS).
**Valor médio Obtido**: 46,4 req/s.
**Diagnóstico**: O sistema não atingiu a carga alvo. A vazão obtida foi aproximadamente 18% do valor solicitado. Isso indica que, sob a carga testada, a aplicação (ou a infraestrutura injetora) não conseguiu processar o volume de requisições esperado.

2. **Análise de Tempo de Resposta (P90)**
**Critério Exigido**: Inferior a 2 segundos (2000ms).
**Valor Médio Obtido**: 7224ms.
**Diagnóstico**: O percentil 90 (P90) foi de 7,2 segundos, o que é 3,6 vezes superior ao limite aceitável. Isso significa que a experiência do usuário final é severamente impactada sob carga, com tempos de espera excessivos.

3. **Conclusão Final**: 
O teste foi concluído com 0.00% de erros, o que demonstra que a aplicação é funcionalmente estável, porém não performática para o cenário de 250 RPS.

**Motivos para o insucesso**:
- **Gargalo de Aplicação/Infra**: O servidor do BlazeDemo pode possuir limitações de recursos (CPU/Memória) ou configurações de servidor web que impedem o processamento de alta concorrência.
- **Latência de Rede**: Por ser um ambiente público, a latência de rede entre a máquina injetora e o servidor impactou diretamente o tempo de resposta acumulado.

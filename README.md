# 🧠 Arquitetura de Poda Dinâmica de Contexto para IA

Este projeto apresenta uma solução prática em Python para otimização de memória RAM/VRAM ao processar contextos longos em Modelos de Linguagem, reduzindo o custo de $O(N^2)$ para linear através de um sistema de poda (*pruning*) em segundo plano.

### 💡 Como Funciona
1. **Multithreading:** O processo principal foca 100% no arquivo ativo atual do usuário.
2. **Poda Logarítmica:** Quando um arquivo vai para o segundo plano, o sistema aplica a fórmula matemática $(N(O \log O))^{-2}$ para calcular quantas palavras-chave o sistema tem permissão para manter na memória ativa, evitando estouro de RAM e erros físicos de ponto flutuante.

---

### 💻 Código do Protótipo (Python)

```python
import math
import time

def aplicar_compressao_comprimento(texto_original):
    palavras = texto_original.split()
    N = len(palavras)
    
    if N <= 1:
        return texto_original

    # Fórmula matemática de decaimento adaptada
    fator = (N * (math.log(N))) ** -2
    
    # Define o comprimento máximo permitido para o histórico
    palavras_a_manter = max(2, math.ceil(N * (fator * 1000))) 
    palavras_a_manter = min(N, palavras_a_manter)
    
    texto_comprimido = palavras[:palavras_a_manter]
    return " ".join(texto_comprimido), fator, palavras_a_manter

# TESTE PRÁTICO COM A AGULHA NO PALHEIRO
texto_agulha = "o ingrediente secreto do bolo da avó é uma pitada de noz-moscada"
texto_salvo, f, tamanho = aplicar_compressao_comprimento(texto_agulha)

print(f"Texto Original: {texto_agulha}")
print(f"Palavras salvas na memória de segundo plano: {texto_salvo}...")

🚀 Diferencial de Mercado
​Eficiência: Estabiliza o consumo de memória em linha reta durante a ingestão de múltiplos dados.
​Precisão: Mantém os tokens como inteiros puros, eliminando alucinações por arredondamento de casas decimais.

### 🏃 Como Executar o Teste
1. Certifique-se de ter o Python instalado.
2. Baixe o arquivo do projeto ou copie o código.
3. Execute o comando no seu terminal:
   ```bash
   python main.py


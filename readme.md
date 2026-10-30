# Coding for Security — Resolução dos Exercícios (2º Semestre)

Resolução dos exercícios da apostila de **Coding for Security** 2º semestre

**Autor:** Amanda · **Turma/RM:** 1TDCPF

---

## Declaração de uso de Inteligência Artificial

Este trabalho foi feito **com a ajuda de IA**

- **Ferramenta:** Claude (Anthropic).
- **Como foi usada:** a IA ajudou a escrever as soluções dos exercícios a incrementação dos scripts de teste e a revisar o código.
- **Minha participação:** [Eu fiz a base dos scripts e fui implementando ao pouco juntamente com a ia e testes]

Declaro o uso de IA por transparência e por integridade acadêmica.

---

## Conteúdo

| Aula | Tema | Exercícios |
|---|---|---|
| 1 | SQL, NoSQL e CAP | 1.1 a 1.3 |
| 2 | MongoDB com PyMongo | 2.1 a 2.3 |
| 3 | MySQL com mysql-connector-python | 3.1 a 3.3 |
| 4 | Machine Learning com scikit-learn | 4.1 a 4.3 |
| 6 | APIs Web com Flask | 6.1 a 6.3 |
| 7 | Flask com MongoDB e MySQL | 7.1 a 7.3 |
| 8 | Web e Segurança (OWASP) | 8.1 a 8.3 |
| 10 | APIs RESTful | 10.1 a 10.3 |
| 11 | Docker com Python | 11.1 a 11.3 |
| 12 | scikit-learn avançado | 12.1 a 12.3 |
| 13 | LLMs para segurança | 13.1 a 13.3 |

---

## Como rodar

```bash
python -m venv .venv
# Windows: .venv\Scripts\activate | Linux/Mac: source .venv/bin/activate
pip install -r requirements.txt
```

Bancos de dados com Docker:

```bash
docker run -d --name mongo-lab -p 27017:27017 mongo:7
docker run -d --name mysql-lab -p 3306:3306 \
  -e MYSQL_ROOT_PASSWORD=senha -e MYSQL_DATABASE=seguranca mysql:8
```

Segredos ficam em variáveis de ambiente, nunca no código:

```bash
export MONGO_URI='mongodb://localhost:27017/'
export MYSQL_PASSWORD='senha'
export OPENAI_API_KEY='sua-chave'   # apenas na Aula 13
```

---

## O que foi testado

| Parte | Como foi testada |
|---|---|
| SQL e MySQL (Aulas 1, 3, 7.3, 8.2) | MariaDB real, compatível com MySQL |
| MongoDB (Aulas 2, 7.1, 7.2) | `mongomock`, que imita o PyMongo |
| Machine Learning (Aulas 4 e 12) | scikit-learn real |
| Flask (Aulas 6 e 8.1) | client de teste do Flask |
| NVD, ipinfo, OpenAI (10.1, 10.3, Aula 13) | respostas simuladas |
| Docker (Aula 11) | cliente Docker simulado |

**Limitações conhecidas:** o Docker não foi testado contra um daemon real, e as chamadas ao NVD, ao ipinfo e à OpenAI foram simuladas. Teste esses pontos no seu ambiente antes de confiar neles.

---

## Observações de segurança

- Todas as consultas SQL com entrada do usuário são **parametrizadas**.
- Nenhuma senha, chave de API ou string de conexão está escrita no código.
- Os exercícios de SQL Injection e prompt injection são **defensivos** e rodam apenas em ambiente local de laboratório.
- Arquivos `.pkl` só são carregados depois de conferir o hash SHA-256.
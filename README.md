# 🛡️ Miniguia: Segurança Avançada em APIs com JWT e Spring Boot

Este repositório é o resultado de um projeto prático desenvolvido para o **Bootcamp GenAI & Dados da DIO**. O objetivo foi utilizar o **NotebookLM** como uma ferramenta de aprendizagem ativa para aprofundar conhecimentos em segurança de aplicações Java, focando em autenticação moderna e mitigação de riscos.

## 📝 Contexto e Objetivos
Como estudante de ADS e interessado em Cyber Security, escolhi o tema de **Segurança em Arquiteturas Web**. O foco central é entender como a implementação de tokens JWT (JSON Web Tokens) no Spring Boot 3.x/6.x pode ser blindada contra ataques comuns listados no OWASP Top 10.

**Objetivos de Estudo:**
- Mapear falhas comuns em implementações de JWT.
- Compreender as proteções nativas do Spring Security 6.
- Explorar como ferramentas de IA podem auxiliar na análise estática de vulnerabilidades.

---

## 📚 Curadoria de Fontes
As fontes utilizadas para alimentar o "cérebro" do NotebookLM foram:
1. **Documentação Oficial Spring Security (OAuth2 Resource Server):** Referência técnica para configuração de filtros e decodificadores.
2. **OWASP Top 10 (2021):** Guia de riscos críticos de segurança em aplicações web.
3. **Artigo Técnico sobre Framework IRIS:** Estudo sobre o uso de LLMs e análise estática (CodeQL) para detecção de falhas de segurança.
4. **RFC 7519 (Padrão JWT):** Documentação técnica que define a estrutura e regras do token.

---

## 🧠 Engenharia de Prompts e "Cicatrizes"

Nesta etapa, testei como a IA reagia a perguntas de complexidade crescente.

### Prompts Utilizados:
1. **Resumo Holístico:** *"Conecte a implementação de JWT no Spring Boot com vulnerabilidades OWASP."*
2. **Análise de Anti-patterns:** *"Liste 5 erros comuns de desenvolvedores ao usar JWT e sugira correções baseadas em SOLID."*
3. **Simulação de Red Team:** *"Descreva um cenário de ataque JWT Kid Injection e como o Spring Security 6.x o mitiga."*

### 🛠️ Cicatrizes e Troubleshooting (O que aprendi no processo):
*   **Desafio de Especificidade:** Inicialmente, a IA forneceu exemplos de configuração baseados em versões antigas do Spring Security (WebSecurityConfigurerAdapter). **Minha correção:** Tive que refinar o prompt exigindo que a resposta considerasse apenas a **versão 6.x**, que utiliza a abordagem baseada em Beans (`SecurityFilterChain`).
*   **Validação de Ferramentas:** A IA mencionou o framework **IRIS**. Como não é uma ferramenta de mercado "comum" como o SonarQube, precisei questionar a IA sobre a origem dessa informação para garantir que não era uma alucinação. Descobri que era um framework de pesquisa acadêmica presente em um dos PDFs que enviei.
*   **O "Pulo do Gato" no JWT:** Notei que a IA deu pouca ênfase inicial à claim `aud` (audiência). Forcei um prompt específico sobre isso e descobri que a falta dessa validação é uma das falhas mais silenciosas em ambientes multi-API.

---

## 📖 Miniguia de Estudo (Entrega Final)

### 1. Resumo Estruturado
A segurança de APIs não deve depender apenas da presença de um token, mas da **validação rigorosa** de sua integridade. No Spring Security 6, a proteção é determinística: o servidor busca chaves públicas em fontes confiáveis (issuer-uri) e ignora instruções maliciosas vindas do cabeçalho do token (como injeções no campo `kid`).

### 2. Glossário de Conceitos Chave
*   **JWT (JSON Web Token):** Padrão para transmissão segura de informações entre partes como um objeto JSON.
*   **KID (Key ID):** Um identificador que indica qual chave deve ser usada para validar a assinatura do token.
*   **Claim:** Uma declaração (informação) contida dentro do token, como o nome do usuário (`sub`) ou permissões (`scp`).
*   **RS256:** Algoritmo de assinatura assimétrica (chave pública/privada) recomendado para JWT.
*   **Resource Server:** No contexto OAuth2, é a nossa API que protege os recursos e valida os tokens.

### 3. Prompts Reutilizáveis para Revisão
*   *"Explique a diferença entre autenticação Stateful e Stateless e por que JWT é o padrão para a segunda."*
*   *"Como implementar a rotação de chaves (Key Rotation) no Spring Security sem derrubar as sessões ativas?"*
*   *"Dê um exemplo de código Java para um `JwtAuthenticationConverter` que mapeia claims customizadas para Roles do Spring Security."*

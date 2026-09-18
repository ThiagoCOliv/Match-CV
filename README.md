# Match-CV
App em desenvolvido com vibe coding para medir e ajustar um currículo para determinada vaga com ats

## Link atual

[https://match-cv.lovable.app](https://match-cv.lovable.app)

PRD feito com gemini

```markdown
# PRD: Match CV & Gerador ATS-Friendly

## 1. Visão Geral do Produto

O **Match CV** é uma aplicação web focada em otimizar currículos para passar pelos filtros automáticos de Applicant Tracking Systems (ATS). A ferramenta analisa a aderência de um currículo a uma vaga específica, destaca lacunas de palavras-chave e reescreve o conteúdo existente para maximizar a pontuação no ATS.

**Regra Absoluta da IA:** A aplicação melhora a clareza, formatação e alinhamento do texto fornecido. **É estritamente proibido inventar experiências, cargos, ferramentas ou competências** não declaradas no currículo original.

---

## 2. Requisitos de UI/UX (Design System & Estilo)

* **Design System:** `shadcn/ui` (Tailwind CSS).
* **Paleta de Cores:**
* **Primária:** Azul (`#2563EB` / `bg-blue-600` e derivados).
* **Fundo/Superfícies:** Branco (`#FFFFFF`) e Cinza Suave (`#F8FAFC`).
* **Acentos:** Azul Escuro para texto e Verde/Amarelo para pontuações/badges.

* **Layout:** Interface limpa de página única com fluxo visual bem definido (Painel Duplo de Entrada $\rightarrow$ Relatório de Match $\rightarrow$ Editor/Exportador).

---

## 3. Fluxo do Usuário & Funcionalidades

### Etapa 1: Entrada de Dados (Input)

* **Componente:** Dois cards lado a lado utilizando `shadcn/ui/card` e `shadcn/ui/textarea`.
* **Painel A:** "Descrição da Vaga" (Textarea com suporte a cola rápida).
* **Painel B:** "Seu Currículo Atual" (Textarea ou upload de `.pdf`/`.txt`).

* **Ação:** Botão principal `shadcn/ui/button` ("Analisar e Otimizar") na cor Azul Primário com estado de carregamento (`spinner`).

### Etapa 2: Painel de Análise (Match & Keywords)

* **Métricas Principais:**
* **Match Score:** `shadcn/ui/progress` exibindo a porcentagem de compatibilidade (ex: 78%).

* **Categorização de Palavras-Chave:**
* **Encontradas:** `shadcn/ui/badge` (variante azul/suave) mostrando termos presentes em ambos.
* **Ausentes no CV:** `shadcn/ui/badge` (variante destrutiva/alerta) destacando termos vitais da vaga que o candidato não citou.

### Etapa 3: Currículo Ajustado (ATS-Friendly)

* **Editor/Visualizador:** Exibição do currículo reformatado com destaque para as palavras-chave incorporadas.
* **Instrução do Modelo de IA (System Prompt Integrado):**
1. Reorganizar seções nos padrões aceitos por ATS (Dados Pessoais, Resumo, Experiência Profissional, Educação, Habilidades).
2. Ajustar verbos de ação e adaptar sinônimos para corresponder à vaga.
3. **Validação de Veracidade:** Manter 100% dos fatos originais sem criar novas atribuições.

* **Exportação:**
* Botão "Copiar Texto Plano".
* Botão "Baixar em PDF (ATS Optimized)" usando layout limpo em coluna única, sem tabelas ou colunas duplas.

---

## 4. Requisitos Técnicos para Lovable

``typescript
// Componentes shadcn/ui obrigatórios
import { Card, CardHeader, CardTitle, CardContent } from "@/components/ui/card"
import { Textarea } from "@/components/ui/textarea"
import { Button } from "@/components/ui/button"
import { Progress } from "@/components/ui/progress"
import { Badge } from "@/components/ui/badge"
import { Tabs, TabsContent, TabsList, TabsTrigger } from "@/components/ui/tabs"
``

* **Estados da Aplicação (`useState` / `useReducer`):**
* `jobDescription`: string
* `rawResume`: string
* `isAnalyzing`: boolean
* `analysisResult`: `{ score: number, matchedKeywords: string[], missingKeywords: string[], optimizedResume: string }`

---

## 5. Critérios de Aceite

1. O usuário consegue colar ambos os textos e obter o resultado em até 10 segundos.
2. A análise identifica corretamente pelo menos 80% das hard e soft skills exigidas no texto da vaga.
3. O texto gerado não contém fatos, métricas ou cargos que não estavam presentes na entrada original do candidato.
4. O documento exportado em PDF utiliza estrutura de coluna única e tipografia padrão amigável para leitura ótica de ATS.
```

# Print da aplicação

<img width="1860" height="2248" alt="image" src="https://github.com/user-attachments/assets/1d601d54-12b3-4cd1-936e-269910e901be" />


# O que o **App de Finanças Pessoais** faz  

- Compara currículo × descrição da vaga.
- Calcula um nível de aderência.
- Mostra competências encontradas e ausentes.
- Sugere melhorias sem inventar experiências.
- Gera uma versão otimizada do currículo para ATS.
- Permite exportar o currículo em PDF ou Word.

# Prompt após o PRD

```
Adição: Exportar o currículo também em .docx, para a pessoa editar antes de enviar
```

# Research Case — Local LLM for Context-Aware Financial Education

## From Financial Data to Contextual Dialogue

### Abstract

Financial information is increasingly available through digital channels, but access to data does not necessarily translate into understanding.

A user may have access to transactions, historical activity, personal profile information and financial products while still lacking an effective mechanism for interpreting this information in context.

This Research Case investigates an alternative approach: using a locally hosted Large Language Model as a conversational layer over structured financial information.

The experiment combines a Streamlit interface, structured JSON and CSV data, contextual prompting and a locally executed `gpt-oss` model through Ollama.

The objective is not to build an autonomous financial advisor or disclose a complete conversational-agent architecture. Instead, the research evaluates whether a local LLM can provide contextual financial education while preserving a clear separation between data, reasoning context and conversational interaction.

The initial results establish technical feasibility and identify important limitations that must be addressed before such a system could evolve toward a production-grade financial platform.

---
# 1. Problem

Financial systems generate large volumes of structured information.

A simplified representation of the available information is:

```text
Customer Profile
       +
Transactions
       +
Historical Activity
       +
Financial Products
       ↓
Financial Context
```

However, structured information is not necessarily understandable information.

A transaction history can show what happened without explaining its broader context.

A product catalogue can describe available products without establishing whether a product is appropriate for a particular situation.

This creates an important distinction:

> **Access to financial data is not equivalent to financial understanding.**

The research therefore investigates whether conversational AI can act as an interface between structured financial information and human interpretation.

---
# 2. Research Question

The central research question is:

> **Can a locally executed Large Language Model use structured customer and financial context to provide useful, contextual financial education through natural-language interaction?**

The question deliberately avoids a more ambitious claim such as:

> "Can an LLM replace a financial advisor?"

That question would require a substantially different level of evidence, governance, validation and domain controls.

This Research Case addresses the narrower and more measurable problem of **contextual financial education**.

---
# 3. Research Hypotheses

The investigation was organized around three dimensions.

## 3.1 Technical Hypothesis

> **H1 — A locally hosted LLM can consume structured financial context and generate conversational responses without requiring the financial data to be sent to an external inference service.**

The hypothesis concerns the technical feasibility of combining:

* structured data;
* contextual prompting;
* local inference;
* conversational interaction.

The experiment therefore investigates the complete flow rather than evaluating the language model in isolation.

---
## 3.2 Operational Hypothesis

> **H2 — Providing the model with explicit customer context can produce responses that are more contextually relevant than a conversation based solely on an isolated user question.**

The operational problem is not simply generating fluent text.

The system must incorporate information such as:

* customer profile;
* transactions;
* historical information;
* available products.

The research therefore treats **context construction** as an important component of the system.

---
## 3.3 Business Hypothesis

> **H3 — A contextual conversational interface can create a potentially useful layer for financial education and engagement, but production value depends on reliability, governance, explainability, security and clearly defined boundaries of use.**

This distinction is essential.

A technically functional conversational interface does not automatically constitute a financial product.

The business question is whether the technology can eventually support a valuable and responsible interaction within a real financial workflow.

---
# 4. Experimental Architecture

The initial architecture was intentionally compact.

```text
User
 │
 ▼
Streamlit
 │
 ▼
Application Layer
 │
 ├── Customer Profile
 ├── Transactions
 ├── Historical Data
 └── Financial Products
 │
 ▼
Context + Prompt
 │
 ▼
HTTP Request
 │
 ▼
Ollama
 │
 ▼
Local LLM
 │
 ▼
Generated Response
 │
 ▼
Streamlit Chat Interface
```

The architecture separates the conversational interface from the local inference layer.

The financial information is represented through structured JSON and CSV sources before being incorporated into the context supplied to the model.

This separation is important because it allows the experiment to investigate the behavior of the LLM without conflating the user interface, data representation and inference mechanism.

---
# 5. Data and Context

The prototype uses four categories of structured information:

```text
JSON
 └── Customer Profile

CSV
 ├── Transactions
 └── Historical Activity

JSON
 └── Financial Products
```

These sources represent different dimensions of context.

### Profile

Provides information necessary to establish the customer's basic context.

### Transactions

Represent current or recent financial activity.

### Historical Data

Provides temporal context that cannot be obtained from an isolated transaction.

### Products

Represent the available financial-product context exposed to the experiment.

The important research variable is therefore not simply the LLM.

It is the combination:

```text
Structured Financial Context
          +
Conversational Query
          ↓
      LLM Response
```

---
# 6. Method

The experiment follows a contextual conversational architecture.

The user interacts through a chat interface.

The application retrieves the structured information required by the experiment and constructs a context for the model.

The context is then submitted to the locally hosted inference service.

The generated response is returned to the conversational interface.

The resulting workflow is:

```text
Question
   ↓
Context Assembly
   ↓
Local Inference
   ↓
Response
   ↓
Human Interpretation
```

The experiment therefore evaluates the complete interaction rather than treating the model as an isolated component.

---
# 7. Research Focus

The investigation does not attempt to optimize every possible dimension of an LLM system.

Instead, it concentrates on four questions:

### Context

Can structured information be incorporated into the interaction?

### Relevance

Does the model use the supplied context when generating a response?

### Interaction

Can users interact with the information through natural language?

### Deployment Model

Can the inference layer operate locally rather than requiring a remote model endpoint?

These questions establish the initial feasibility boundary.

---
# 8. Results

The prototype demonstrated the complete technical path from structured financial information to conversational interaction:

```text
Financial Data
      ↓
Context
      ↓
Prompt
      ↓
Local HTTP Inference
      ↓
gpt-oss
      ↓
Conversational Response
```

The experiment therefore established that the proposed architecture can function as a local conversational interface over structured financial data.

The most relevant result is not simply that a response was generated.

The experiment demonstrated the integration of:

* structured customer context;
* transaction information;
* historical information;
* financial-product information;
* local LLM inference;
* conversational interaction.

This establishes the initial technical feasibility of the approach.

### Quantitative Results

Recommended presentation:

| Dimension            | Experimental Result                                                                                                                                                                                                                           |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Local Execution      | `The model was run locally, demonstrating the viability of the architecture without relying on an external inference API.`                                                                                                                    |
| Response generation  | `The questions and answers demonstrated behavior appropriate to the defined guardrails; however, further testing is needed to more broadly assess consistency, limits, and behavior in different scenarios.`                                  |
| Context integration  | `Adequate. The system successfully used the structured context provided by the application to support conversational interaction.`                                                                                                            |
| Interaction          | `Suitable. The conversational interface allowed interaction with the model based on the information provided by the system.`                                                                                                                  |
| Resource consumption | `High for the environment used. Local execution of the model consumed a large portion of the available computer memory, demonstrating that local inference requires computational capacity compatible with the model and configuration used.` |

---
# 9. What the Experiment Demonstrated

The experiment establishes three important observations.

### 9.1 Local inference is technically feasible

A conversational application can communicate with a locally hosted LLM through an HTTP inference layer.

This creates an architecture in which the model execution does not inherently depend on a remote commercial inference endpoint.

---
### 9.2 Structured information can become conversational context

Financial information traditionally represented as JSON or CSV can be incorporated into an interaction model based on natural language.

This creates a different access pattern:

```text
Traditional

Data
 ↓
Query
 ↓
Result


Conversational

Question
 ↓
Context
 ↓
Interpretation
 ↓
Response
```

The second approach can potentially reduce the interaction barrier for users who are not comfortable working directly with structured financial information.

---
### 9.3 The model is not the complete system

The experiment also exposes an important limitation.

The LLM does not independently constitute the financial solution.

A production system would require additional layers for:

* data governance;
* authorization;
* privacy;
* security;
* traceability;
* validation;
* monitoring;
* model evaluation;
* policy enforcement;
* responsible use.

Therefore:

> **The LLM is an inference component inside the system, not the system itself.**

---
# 10. Business Interpretation

The potential business value is not simply "chat with an LLM."

The more relevant opportunity is the transformation of complex financial information into a more accessible interaction model.

Conceptually:

```text
Financial Information
        ↓
Contextual Interpretation
        ↓
Conversational Interaction
        ↓
Financial Understanding
```

This may create opportunities in areas such as:

* financial education;
* customer engagement;
* information discovery;
* contextual explanation;
* financial-service interfaces.

However, these are **potential application areas**, not validated product-market opportunities.

The experiment alone cannot establish willingness to pay, regulatory viability, customer adoption or economic return.

Those questions require separate validation.

---
# 11. What We Deliberately Do Not Claim

This Research Case does not claim that the prototype:

* provides regulated financial advice;
* replaces a financial professional;
* produces investment recommendations;
* guarantees factual correctness;
* eliminates hallucination;
* provides production-grade financial security;
* satisfies regulatory requirements;
* represents a validated commercial product.

These boundaries are deliberate.

The objective is to establish technical feasibility and identify the next research questions.

---
# 12. Engineering Limitations

A local LLM architecture introduces its own engineering constraints.

Among the relevant questions are:

```text
Model Quality
      ↓
Context Quality
      ↓
Response Reliability
      ↓
Validation
      ↓
Security
      ↓
Observability
      ↓
Operational Scalability
```

A successful demonstration at prototype scale does not establish production readiness.

In particular, a financial system requires stronger controls around the relationship between generated content and authoritative financial information.

The system must eventually distinguish between:

```text
Source Data
     │
     ▼
Derived Information
     │
     ▼
Model Interpretation
     │
     ▼
Generated Language
```

That distinction becomes increasingly important as the system moves from education toward decision support.

---
# 13. Strategic Evolution

The current architecture should therefore be viewed as the first layer of a larger research program.

```text
Current Prototype
       │
       ▼
Contextual Financial Education
       │
       ▼
Reliable Context Retrieval
       │
       ▼
Response Evaluation
       │
       ▼
Governance & Traceability
       │
       ▼
Domain-Specific Decision Support
       │
       ▼
Production System
```

Each stage introduces a new engineering and business question.

The objective is not to prematurely build the entire platform.

It is to validate each layer before increasing system complexity.

---
# 14. Research-to-Product Perspective

The prototype also reveals a broader product hypothesis.

The opportunity may not be:

> **"an application that sends prompts to an LLM."**

That architecture is increasingly accessible.

The potential differentiation lies in the layers surrounding the model:

```text
                DOMAIN
                  │
                  ▼
             DATA CONTEXT
                  │
                  ▼
            AI / INFERENCE
                  │
                  ▼
          VALIDATION / POLICY
                  │
                  ▼
             USER ACTION
                  │
                  ▼
          BUSINESS OUTCOME
```

This is where future research should concentrate.

The model can change.

The engineering problem remains.

---
# 15. What Needs to Evolve

The experiment establishes feasibility, not completion.

The next research stages should investigate at least:

### Context reliability

How can the system ensure that the generated response remains grounded in authoritative financial information?

### Response evaluation

How can correctness, relevance and consistency be evaluated systematically?

### Governance

How can the system distinguish educational information from advice or recommendation?

### Security

How should sensitive financial information be protected throughout the application and inference lifecycle?

### Traceability

How can the system establish which data and context contributed to a generated response?

### Observability

How can model, application and inference behavior be monitored?

### Business validation

Which real financial workflow benefits sufficiently from this interaction model to justify adoption?

These questions define the next stage of research.

---
# 16. Strategic Conclusion

This Research Case demonstrates a small but important architectural transition:

> **from financial data interfaces to contextual financial interaction.**

The experiment shows that structured financial information can be combined with local LLM inference to create a conversational interface capable of interpreting a defined context.

However, the experiment also demonstrates why an LLM alone is not a financial solution.

The relevant engineering challenge is the system surrounding the model:

```text
Data
 +
Context
 +
Inference
 +
Validation
 +
Security
 +
Governance
 +
Observability
 =
AI System
```

The prototype therefore represents an initial research milestone rather than a finished product.

Its strategic value lies in establishing the feasibility of the architecture while exposing the next set of technical, operational and business questions.

The next stage should not be to simply add more prompts.

It should be to determine **how a conversational financial system can remain grounded, traceable, secure and useful as the complexity of the domain increases.**

---
## Research Status

**Stage:** Experimental Prototype

**Domain:** Financial Education / Conversational AI

**Inference:** Local LLM

**Interface:** Streamlit

**Structured Context:** JSON + CSV

**Inference Layer:** Ollama

**Model:** gpt-oss

**Current Objective:** Technical feasibility and research foundation

**Product Status:** Prototype

**Commercial Status:** Not validated

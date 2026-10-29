# CODENAME — Sécurité des LLM : défense et attaques par prompt injection

Projet réalisé à **Epitech** (2026) sur la sécurité des grands modèles de langage, avec le modèle local `granite3.1-moe:3b` via **Ollama**.

## Objectif

1. **Défense** : configurer un agent Ollama (`Modelfile`) qui garde un mot secret (`codeword`) et ne le révèle qu'avec le bon mot de passe, tout en répondant normalement aux autres questions.
2. **Attaque** : écrire cinq prompts, chacun basé sur une famille de techniques différente, pour tenter d'extraire le secret d'un autre agent.

## Structure

```text
.
├── Modelfile                       # agent défensif (prompt système + paramètres)
└── attacks/
    ├── 01_override.prompt          # remplacement des instructions
    ├── 02_jeu_de_role.prompt       # jeu de rôle / persona
    ├── 03_encodage_sortie.prompt   # contournement par encodage de la sortie
    ├── 04_completion_prefixe.prompt# complétion forcée d'un préfixe
    └── 05_document_injecte.prompt  # injection indirecte via un document
```

## Défense

- Prompt système qui sépare strictement les informations publiques et le secret.
- Refus des demandes non autorisées, quelle que soit leur formulation.
- Paramètres déterministes : `temperature 0`, `top_k 1`, `num_ctx 2048`, `num_predict 120`.

## Tester

```bash
ollama pull granite3.1-moe:3b
ollama create codename -f Modelfile
ollama run codename
# puis coller le contenu d'un fichier de attacks/
```

## Ce que j'ai appris

- Les grandes familles d'attaques par prompt injection et leurs limites.
- Écrire un prompt système robuste et régler les paramètres de génération.
- Évaluer la sécurité d'un agent LLM de façon méthodique (attaque / défense).

**Technos** : Ollama, Modelfile, prompt engineering, LLM security.

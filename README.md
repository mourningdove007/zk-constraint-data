# ZK Constraint Dataset

A dataset of Circom circuit examples for fine-tuning LLMs to identify insufficient constraints in ZK proof systems.

## v0.0 (proof of concept)

These 15 training examples and 4 validation examples are far from sufficient to train a quality model. A model fine-tuned on this little data will likely only behave sensibly on very simple circuits.

## Data Sources

Current examples are mostly circuits written specifically for this dataset. The repository owner received permission from ZKSecurity to use their public audit findings as training data; those rows live in `zk_security.jsonl`. Those examples include a `source` object (name, link, protocol) so readers can open the underlying report. There are currently 3 examples from ZKSecurity; we plan to add more as we read additional reports. 

## Data Format

Each line in the JSONL file is a complete training example. Rows derived from ZKSecurity include a `source` object; synthetic examples may omit it.

```json
{
  "messages": [
    {"role": "system", "content": "You are a Zero-Knowledge Proof security auditor specializing in Circom. Your goal is to identify under-constrained signals and logical vulnerabilities in circuits."},
    {"role": "user", "content": "Audit this circuit for vulnerabilities:\n\n```circom\n...```"},
    {"role": "assistant", "content": "Vulnerability: ...\n\nExplanation: ...\n\nFix: ..."}
  ],
  "source": {
    "name": "...",
    "link": "https://...",
    "protocol": "..."
  }
}
```

## Related

- Hugging Face dataset: [mourningdove/zk-constraint-data](https://huggingface.co/datasets/mourningdove/zk-constraint-data)

## Deploying

To deploy a new version of the dataset, we use the following command:

```
hf upload mourningdove/zk-constraint-data . --repo-type=dataset
```



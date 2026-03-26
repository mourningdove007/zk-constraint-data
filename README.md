# ZK Constraint Dataset

A curated dataset of Circom circuit examples for fine-tuning LLMs to identify insufficient constraints in ZK proof systems.



## Vulnerability Patterns Covered

| # | Pattern | What is missing or weakened |
|---|---|---|
| 1 | Hint without recomposition | `<--` with no binding `===` |
| 2 | Boolean check only | `x * (x-1) === 0` but x is never tied to source |
| 3 | Underdetermined system | 1 equation, 2 unknowns |
| 4 | Weak final check | `a * b === 0` instead of `a === 0` |
| 5 | Missing range constraint | bits decomposed but never bounded |
| 6 | Unconstrained output | output assigned with `<--` not `<==` |
| 7 | Partial constraint | only some iterations constrained in a loop |
| 8 | Missing input validation | signal used before being constrained |
| 9 | Reused signal across contexts | same signal constrained differently in two places |
| 10 | Unconstrained intermediate | intermediate value computed but never tied to output |

## Data Format

Each line in the JSONL file is a complete training example:

```json
{
  "messages": [
    {"role": "system", "content": "YYou are a Zero-Knowledge Proof security auditor specializing in Circom. Your goal is to identify under-constrained signals and logical vulnerabilities in circuits."},
    {"role": "user", "content": "Audit this circuit for vulnerabilities:\n\n```circom\n...```"},
    {"role": "assistant", "content": "Vulnerability: ...\n\nExplanation: ...\n\nFix: ..."}
  ],
  "source": {
    "name": "...",
    "link": "circom",
    "protocol": "...",
  }
}
```

## Data Sources

Current examples are original synthetic circuits written specifically for this dataset. Future examples sourced from public repositories will include full attribution in the `origin` block with the applicable license noted. Only data we create or have explicit permission from the dataset owner will be allowed for training purposes.

## Related

- Hugging Face dataset: [mourningdove/zk-constraint-data](https://huggingface.co/datasets/mourningdove/zk-constraint-data)

## Deploying

To deploy a new version of the dataset, we use the following command:

```
hf upload mourningdove/zk-constraint-data . --repo-type=dataset
```


## V 0.0 (Proof Of Concept)

We have 16 synthetic examples to avoid using the intelectual property of datasets. The owner of this repository was given permission from ZKSecurity to use their audit reports as training data. These are located in `zk_security.jsonl`.

# We Found an Infinite Benchmark Glitch: Dynamic N-Dimensional Grid Regression (DNDGR) Benchmark

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

## Introduction

This repository contains the code and documentation for the **Dynamic N-Dimensional Grid Regression (DNDGR)** benchmark, a novel and infinitely scalable benchmark designed to evaluate the in-context learning capabilities of Large Language Models (LLMs).

The DNDGR benchmark challenges LLMs to learn and generalize from in-context examples of sequences generated from an n-dimensional grid of words (or other symbols). The complexity of the task can be dynamically adjusted by varying the dimensionality of the grid, its size, the sequence generation rules, and the level of noise. This makes it virtually impossible for models to "cheat" by memorizing solutions and allows for a continuous assessment of LLMs' abilities as they improve.

**This benchmark is inspired by the paper ["ICLR: In-Context Learning of Representations"](https://arxiv.org/abs/2501.00070).**

## Why DNDGR?

Traditional LLM benchmarks often suffer from several limitations:

*   **Saturation:** Models eventually achieve near-perfect performance, making it difficult to differentiate their capabilities.
*   **Memorization:** Models might memorize solutions from the training data, leading to inflated performance.
*   **Lack of Focus on In-Context Learning:** Many benchmarks do not specifically target the ability of LLMs to learn from context without weight updates.

The DNDGR benchmark addresses these limitations by:

*   **Infinite Scalability:** The complexity of the tasks can be scaled indefinitely, ensuring that the benchmark remains challenging even for future, more powerful LLMs.
*   **Dynamic Task Generation:** New tasks are generated on the fly, preventing memorization and requiring genuine generalization.
*   **Focus on In-Context Learning:** The benchmark directly assesses the model's ability to learn from in-context examples.
*   **Measuring Learning Efficiency:** It measures not only accuracy but also how quickly models learn and adapt.

## Benchmark Details

### Grid Construction

*   **Dimensionality (n):** The number of dimensions of the grid (e.g., 1D, 2D, 3D, ...).
*   **Size (N):** The size of the grid along each dimension (assuming all dimensions have the same size).
*   **Vocabulary (V):** A set of unique words or symbols that populate the grid.
*   **Word Representation:** Words can be represented by indices or embeddings.

### Sequence Generation

*   **Starting Point:** A random cell in the grid.
*   **Movement Rules:**
    *   **Dimension Choice:** Randomly choose a dimension (e.g., X, Y, Z).
    *   **Direction:** Move in either the +1 or -1 direction along the chosen dimension.
*   **Sequence Length:** The number of steps in the generated sequence.
*   **Boundary Conditions:** Define whether sequences wrap around or stop at the grid's edges.

### Task

The LLM is given a context consisting of example sequences generated from the grid. The task is to predict the next word in a new sequence based on the learned movement rules.

### Complexity Control

*   **Dimensionality (n):** Higher dimensions make the task exponentially harder.
*   **Grid Size (N):** Larger grids increase the number of possible states and relationships.
*   **Sequence Length:** Longer sequences require tracking more complex trajectories.
*   **Noise:** Introduce noise through movement errors, word swaps, or missing words.
*   **Number of In-Context Examples:** Fewer examples make the task harder.

### Evaluation Metrics

*   **Accuracy:** Percentage of correctly predicted next words.
*   **Convergence Speed:** Number of in-context examples needed to reach a target accuracy.
*   **Regret:** Cumulative difference between the model's predictions and optimal predictions.
*   **Area Under the Learning Curve (AULC):** Area under the curve of accuracy vs. number of examples.
*   **Sample Efficiency:** Data needed to reach a certain performance threshold.

## Getting Started

### Installation

```bash
git clone https://github.com/kreasof-ai/infinite-benchmark-glitch
cd infinite-benchmark-glitch
pip install -r requirements.txt
```

### Usage

#### Running the Benchmark

```bash
python run_benchmark.py --config config.yaml
```

`config.yaml` is a configuration file that specifies the benchmark parameters (see `config.yaml.example` for an example).

#### Generating New Tasks

```bash
python generate_tasks.py --config config.yaml
```

#### Evaluating a New Model

1. Implement a new model class that inherits from `models.BaseModel`.
2. Add your model to `models/__init__.py`.
3. Run the benchmark with your model using the `--model` flag.

## Configuration

The `config.yaml` file allows you to customize various aspects of the benchmark:

*   `dimensionality`: Number of dimensions.
*   `grid_size`: Size of the grid in each dimension.
*   `vocab_size`: Size of the vocabulary.
*   `sequence_length`: Length of the generated sequences.
*   `noise_level`: Probability of introducing noise.
*   `num_examples`: Number of in-context examples.
*   `max_examples`: Maximum number of in-context examples to use (for convergence tests).
*   `target_accuracy`: Target accuracy for convergence tests.
*   `num_trials`: Number of trials to run for each setting.

## Limitations

### Dependency on Pure Autoregressive Inference

The DNDGR benchmark is designed to evaluate the in-context learning capabilities of LLMs operating in a **purely autoregressive, sequential generation mode, without access to external tools or the ability to modify their prompt**. This is a crucial constraint. 

**LLMs that can generate code to search within the context or retrieve information from external sources could potentially "cheat" on this benchmark by simply looking up the answers in the provided examples, rather than learning the underlying relationships between words in the grid.**

Therefore, the DNDGR benchmark, in its current form, is **most suitable for evaluating models that operate solely based on the provided context and generate text sequentially without external tool use.** It might not accurately assess the in-context learning abilities of models that deviate from this pure autoregressive paradigm.

### Mitigation Strategies

While this limitation cannot be entirely eliminated without fundamentally altering the way LLMs are used, we suggest the following to mitigate its impact:
1. **Careful Model Selection:** Prioritize the evaluation on LLMs known to be primarily autoregressive and not designed for external tool use. Report if any external tool is used.
2. **Transparency:**  Clearly state in the reported results whether the evaluated models adhere to the pure autoregressive constraint.

We acknowledge this limitation and encourage the community to explore alternative benchmark designs that are robust to these challenges. Future work could also involve developing methods for detecting and preventing such "cheating" behaviors during evaluation.

## Contributing

We welcome contributions to the DNDGR benchmark! If you have any ideas for improvements or new features, please feel free to open an issue or submit a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Citation

If you use this benchmark in your research, please cite:

```
@article{dndgrbenchmark,
  title={We Found an Infinite Benchmark Glitch: Dynamic N-Dimensional Grid Regression (DNDGR) Benchmark},
  author={Habibullah Akbar},
  year={2025},
}
```

## Acknowledgements

```
@misc{park2024iclrincontextlearningrepresentations,
      title={ICLR: In-Context Learning of Representations}, 
      author={Core Francisco Park and Andrew Lee and Ekdeep Singh Lubana and Yongyi Yang and Maya Okawa and Kento Nishi and Martin Wattenberg and Hidenori Tanaka},
      year={2024},
      eprint={2501.00070},
      archivePrefix={arXiv},
      primaryClass={cs.CL},
      url={https://arxiv.org/abs/2501.00070}, 
}
```
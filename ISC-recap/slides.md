---
marp: true
style: |
    section.centered {
        display: flex;
        flex-direction: column;
        justify-content: center;
        text-align: center;
        width: auto;
    }
---

<!-- _class: centered -->

# My ISC conference

A recap of what I discovered during ISC attendance

---

## Table of contents

1. Leveraging and Evaluating LLMs for HPC Research


2. An Introduction to Developing Highly Parallel Applications Using C++ and SYCL

---

<!-- _class: centered -->

# 1. Leveraging and evaluating LLMs for HPC research

---

<!-- _class: centered -->

## Introduction to LLMs

---

<!-- _class: centered -->

<img src="./img/transformer.png">

---

## What are parameters?

- The weights, which control how information propagates between layers.


- The biases, which offset the values associated with the activation functions.


- Layer normalization weights.


- The embedding matrices, $W_{emb} \in \mathbb{R}^{|V|\times d}$, where $|V|$ is the size of the vocabulary and $d$ the dimensionality of the associated vector representation.

---

<!-- _class: centered -->

## In autoencoder-decoder architectures *more parameters* = *more capabilities* but harder training phase.

---

## Multimodality

Now flagship models are boasting multimodal capacities, therefore the model is able to manipulate different forms of media:

- Text
- Audio
- Video
- Images

This can be done through the same A/D architecture by predicting the next most probable byte in the sequence (for example for images) another archetype that is rapidly gaining traction is the one of Diffusion Models.

---

<!-- _class: centered -->

<img src="./img/diffusion_models.png">

___

<!-- _class: centered -->

## LLMs in HPC

---

<!-- _class: centered -->

<img src="./img/llms_hpc.png">

___

<!-- _class: centered -->

## How to effectively generate code with LLMs

###### Reminder: if we are working with a language that doesn't have a high usage rate then the result is going to be heavily affected (e.g. newer c++ standards).

Example applied to the linear heat diffusion equation.

---

<!-- _class: centered -->

<img src="./img/heat_1.png">

___

<!-- _class: centered -->

<img src="./img/heat_2.png">

___

<!-- _class: centered -->

<img src="./img/heat_3.png">

___

<!-- _class: centered -->

<img src="./img/heat_4.png">

___

<!-- _class: centered -->

<img src="./img/heat_5.png">

___

<!-- _class: centered -->

<img src="./img/heat_6.png">

___

## Main takeaways

1. Claude is capable to generate code that can solve the problem with a high level of accuracy (absolute error between $10^{-10}$ and $10^{-18}$).
2. It's an extremely easy problem, probably fished some solutions from *training memory*, therefore this is not as indicative as it might be regarding real world performance.
3. The process that took from beginning of the problem to solution involved a series of steps that made each task easier for the LLM.

---

<!-- _class: centered -->

<img src="./img/translation.png">

___

<!-- _class: centered -->

<img src="./img/algorithm_design.png">

___

## Achievements of AlphaEvolve

Found better algorithms for:

1. Data center scheduling,

2. Highly optimized arithmetic circuit for matrix multiplication in TPU,

3. Flash Attention kernel implementation in Transformer,

3. Matrix Multiplications (improved Strassen algorithm for 4x4) \[Nov25\].

---

<!-- _class: centered -->

## Prompting

---

<!-- _class: centered -->

<img src="./img/prompting.png">

___

<!-- _class: centered -->

<img src="./img/good_prompting.png">

___

<!-- _class: centered -->

<img src="./img/prompt_bts.png">

___

<!-- _class: centered -->

<img src="./img/gp_example.png">

___

<!-- _class: centered -->

<img src="./img/advanced_prompting.png">

___

## Few-shot prompting

Few-shot prompting means giving the LLM some examples of what kind of output we would like, based on some examples, to steer its responses towards the correct direction.

Few-shots is used also as a measurement of the performance of the model, usually this metric answers to the question 'How many hints did we have to give the LLM to make sure that its answer was right?'. There are many variation of this same metric that are more focused on how accurate the answer is based on the number of hints (like 0-shot and 1-shot).

___

<!-- _class: centered -->

## Performance evaluation

---

<!-- _class: centered -->

<img src="./img/testing_1.png">

___

<!-- _class: centered -->

<img src="./img/testing_2.png">

---

<!-- _class: centered -->

<img src="./img/advanced_math.png">

---

<!-- _class: centered -->

<img src="./img/what_to_test.png">

---

<!-- _class: centered -->

## The machine learning problem

Suppose we train a model $\mathcal{M}$ on a set $T$, when we analyze the performance of such model it's important that the dataset utilized $V$ doesn't contain samples from $T$, otherwise the model will already know the ground truth for such test samples and therefore the performance analysis will return an overconfident estimate of the model's capabilities.

---

## How to test

LLMs can be asked to reply to multiple choice questions or questions that require the generation of a short essay, this leads to an analysis of how how specific or broad the knowledge of the model is, as well as its ability to reason on a certain task.

Some classical ways of evaluating performance are:

- 0 shot evaluation,
- 1-5 shot evaluation (few shot),
- Joint performance evaluation for multiple choice,
- Multiple choice but split the answers in different prompts.

---

<!-- _class: centered -->

<img src="./img/how_to_test.png">

---

<!-- _class: centered -->

<img src="./img/llm_judge.png">

---

<!-- _class: centered -->

## LLM boosted research

---

<!-- _class: centered -->

<img src="./img/uncertainty.png">

---

## Handling uncertainty in LLMs

At the current stage of this technology uncertainty is a very important topic because:

1. LLMs hallucinate and tend on giving confident responses even if they have no clue what they are talking about.

2. Chain of thought and other frameworks suggest to use multiple different prompts to make the answer better, but what happens to the uncertainty of the answer? Since successive prompts are not independent from each other, how can we modellize uncertainty propagation?

---

<!-- _class: centered -->

<img src="./img/workflow.png">

---

<!-- _class: centered -->

## Research example on transionic flow

---

<!-- _class: centered -->

<img src="./img/research_example_1.png">

---

<!-- _class: centered -->

<img src="./img/research_example_2.png">

---

<!-- _class: centered -->

<img src="./img/research_example_3.png">

---

<!-- _class: centered -->

<img src="./img/argonne_o1.png">

---

<!-- _class: centered -->

<img src="./img/argonne_2025.png">

---

<!-- _class: centered -->

<img src="./img/AI_boosted_publication.png">

---

<!-- _class: centered -->

<img src="./img/example_workflow.png">

---

<!-- _class: centered -->
## An Introduction to Developing Highly Parallel Applications Using C++ and SYCL

---

<!-- _class: centered -->

<img src="./img/what-is-sycl.png">

---

<!-- _class: centered -->

<img src="./img/sycl-compile.png">

---

- SYCL offers interoperability with a wide variety of backends and devices, some of the most notable available are OpenCL, CUDA, HIP, OpenMP.
- SYCL offers high level abstractions that work independently of the platform the code is being run on.
- SYCL 2020 is based on the 2017 standard for C++. It has no `pragma`, language extensions or mandatory attributes.

---

<!-- _class: centered -->

<img src="./img/sycl-interface.png">

---

<!-- _class: centered -->

<img src="./img/sycl-compile-model.png">

---

<!-- _class: centered -->

<img src="./img/sycl-queues.png">

---

## Memory models

SYCL has two different ways of managing data:
- buffer / accessor,
- Unified Shared Memory.

While during the speech we used the buffer / accessor model the speakers stressed the concept that buffer accessors are a very useful high-level abstraction to get started, but once things get serious they become pretty much useless.

The buffer / accessor model in SYCL leverages lazy memory movement so that informations are passed ot the device only once the device really needs them.

---

<!-- _class: centered -->

<img src="./img/buffer-accessor.png">

---

<!-- _class: centered -->

<img src="./img/usm-malloc-device.png">

---

## Other USM operations

- Asynchronous `memcpy`
```c++
event queue::memcpy(void* dest, const void* src, size_t numBytes, const std::vector &depEvents);
```

- Synchronous `free`
```c++
void free(void* ptr, queue& syclQueue);
```

---

## SYCL execution model

SYCL's execution model rips off NVIDIA's execution model following a similar structure, this is not due to a lack of fantasy but it's done to make sure that the high-level abstraction is not forcefully connected to any specific vendor's.

- Single threads are renamed _work-items_, they are the smalles unit of processing.
- Work-items are grouped in _work-groups_, as for NVIDIA's blocks the number of work-groups that can concurrently operate on the machine is heavily dependent on resources used.
- Work-groups are clustered in _ND-ranges_.

---

<!-- _class: centered -->

<img src="./img/sycl-nd-range.png">

---

## SYCL kernel as function object

SYCL kernels can be expressed either as lambdas or as function objects, kernel arguments are passed
as capture targets or as data members.

```c++
class MyKernel {
  sycl::accessor input_;
  float* output_;

  MyKernel(sycl::buffer buf, float* output, sycl::handler& h)
    : input{buf.get_access(h)}, output_{output} {}

  // const is required
  void operator()(sycl::item<1> i) const {
    ; // computation here
  }
};
```

---

## SYCL kernel as a lambda function

```c++
sycl::buffer buf = /* normal init */;
float * output = sycl::malloc_device(/* params */);

... queue submit as normal ...

auto acc = buf.get_access(h);
auto func = [=](sycl::item<1> i) {
  acc[i] = someVal;
  output[i.get_global_linear_id()] = someOtherVal;
});
handler.parallel_for(range, func);
```

---

## Sources

**\[Nov25\]** :: Alexander Novikov et al.; *AlphaEvolve: A coding agent for scientific and algorithmic discovery* June 2025 Arxiv preprint [doi](https://doi.org/10.48550/arXiv.2506.13131)

---



























<!-- _class: centered -->

<img src="./img/llm_training.png">

---


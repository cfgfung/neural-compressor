<div align="center">

Intel® Neural Compressor
===========================
<h3> An open-source Python library supporting popular model compression techniques on all mainstream deep learning frameworks (TensorFlow, PyTorch, ONNX Runtime, and MXNet)</h3>

[![python](https://img.shields.io/badge/python-3.7%2B-blue)](https://github.com/intel/neural-compressor)
[![version](https://img.shields.io/badge/release-2.3-green)](https://github.com/intel/neural-compressor/releases)
[![license](https://img.shields.io/badge/license-Apache%202-blue)](https://github.com/intel/neural-compressor/blob/master/LICENSE)
[![coverage](https://img.shields.io/badge/coverage-85%25-green)](https://github.com/intel/neural-compressor)
[![Downloads](https://static.pepy.tech/personalized-badge/neural-compressor?period=total&units=international_system&left_color=grey&right_color=green&left_text=downloads)](https://pepy.tech/project/neural-compressor)

[Architecture](./docs/source/design.md#architecture)&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;[Workflow](./docs/source/design.md#workflow)&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;[Results](./docs/source/validated_model_list.md)&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;[Examples](./examples/README.md)&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;[Documentations](https://intel.github.io/neural-compressor)

---
<div align="left">

Intel® Neural Compressor aims to provide popular model compression techniques such as quantization, pruning (sparsity), distillation, and neural architecture search on mainstream frameworks such as [TensorFlow](https://www.tensorflow.org/), [PyTorch](https://pytorch.org/), [ONNX Runtime](https://onnxruntime.ai/), and [MXNet](https://mxnet.apache.org/),
as well as Intel extensions such as [Intel Extension for TensorFlow](https://github.com/intel/intel-extension-for-tensorflow) and [Intel Extension for PyTorch](https://github.com/intel/intel-extension-for-pytorch).
In particular, the tool provides the key features, typical examples, and open collaborations as below:

* Support a wide range of Intel hardware such as [Intel Xeon Scalable Processors](https://www.intel.com/content/www/us/en/products/details/processors/xeon/scalable.html), [Intel Xeon CPU Max Series](https://www.intel.com/content/www/us/en/products/details/processors/xeon/max-series.html), [Intel Data Center GPU Flex Series](https://www.intel.com/content/www/us/en/products/details/discrete-gpus/data-center-gpu/flex-series.html), and [Intel Data Center GPU Max Series](https://www.intel.com/content/www/us/en/products/details/discrete-gpus/data-center-gpu/max-series.html) with extensive testing; support AMD CPU, ARM CPU, and NVidia GPU through ONNX Runtime with limited testing

* Validate popular LLMs such as [LLama2](/examples/pytorch/nlp/huggingface_models/language-modeling/quantization/llm), [Falcon](/examples/pytorch/nlp/huggingface_models/language-modeling/quantization/llm), [GPT-J](/examples/pytorch/nlp/huggingface_models/language-modeling/quantization/llm), [Bloom](/examples/pytorch/nlp/huggingface_models/language-modeling/quantization/llm), [OPT](/examples/pytorch/nlp/huggingface_models/language-modeling/quantization/llm), and more than 10,000 broad models such as [Stable Diffusion](/examples/pytorch/nlp/huggingface_models/text-to-image/quantization), [BERT-Large](/examples/pytorch/nlp/huggingface_models/text-classification/quantization/ptq_static/fx), and [ResNet50](/examples/pytorch/image_recognition/torchvision_models/quantization/ptq/cpu/fx) from popular model hubs such as [Hugging Face](https://huggingface.co/), [Torch Vision](https://pytorch.org/vision/stable/index.html), and [ONNX Model Zoo](https://github.com/onnx/models#models), by leveraging zero-code optimization solution [Neural Coder](/neural_coder#what-do-we-offer) and automatic [accuracy-driven](/docs/source/design.md#workflow) quantization strategies

* Collaborate with cloud marketplaces such as [Google Cloud Platform](https://console.cloud.google.com/marketplace/product/bitnami-launchpad/inc-tensorflow-intel?project=verdant-sensor-286207), [Amazon Web Services](https://aws.amazon.com/marketplace/pp/prodview-yjyh2xmggbmga#pdp-support), and [Azure](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/bitnami.inc-tensorflow-intel), software platforms such as [Alibaba Cloud](https://www.intel.com/content/www/us/en/developer/articles/technical/quantize-ai-by-oneapi-analytics-on-alibaba-cloud.html), [Tencent TACO](https://new.qq.com/rain/a/20221202A00B9S00) and [Microsoft Olive](https://github.com/microsoft/Olive), and open AI ecosystem such as [Hugging Face](https://huggingface.co/blog/intel), [PyTorch](https://pytorch.org/tutorials/recipes/intel_neural_compressor_for_pytorch.html), [ONNX](https://github.com/onnx/models#models), [ONNX Runtime](https://github.com/microsoft/onnxruntime), and [Lightning AI](https://github.com/Lightning-AI/lightning/blob/master/docs/source-pytorch/advanced/post_training_quantization.rst)

## Installation

### Install from pypi
```Shell
pip install neural-compressor
```
> [!NOTE]
> More installation methods can be found at [Installation Guide](https://github.com/intel/neural-compressor/blob/master/docs/source/installation_guide.md). Please check out our [FAQ](https://github.com/intel/neural-compressor/blob/master/docs/source/faq.md) for more details.

## Getting Started
### Quantization with Python API

```shell
# Install Intel Neural Compressor and TensorFlow
pip install neural-compressor
pip install tensorflow
# Prepare fp32 model
wget https://storage.googleapis.com/intel-optimized-tensorflow/models/v1_6/mobilenet_v1_1.0_224_frozen.pb
```
```python
from neural_compressor.data import DataLoader, Datasets
from neural_compressor.config import PostTrainingQuantConfig

dataset = Datasets("tensorflow")["dummy"](shape=(1, 224, 224, 3))
dataloader = DataLoader(framework="tensorflow", dataset=dataset)

from neural_compressor.quantization import fit

q_model = fit(
    model="./mobilenet_v1_1.0_224_frozen.pb",
    conf=PostTrainingQuantConfig(),
    calib_dataloader=dataloader,
)
```

## Documentation

<table class="docutils">
  <thead>
  <tr>
    <th colspan="8">Overview</th>
  </tr>
  </thead>
  <tbody>
    <tr>
      <td colspan="2" align="center"><a href="./docs/source/design.md#architecture">Architecture</a></td>
      <td colspan="2" align="center"><a href="./docs/source/design.md#workflow">Workflow</a></td>
      <td colspan="2" align="center"><a href="examples/README.md">Examples</a></td>
      <td colspan="2" align="center"><a href="https://intel.github.io/neural-compressor/latest/docs/source/api-doc/apis.html">APIs</a></td>
    </tr>
  </tbody>
  <thead>
    <tr>
      <th colspan="8">Python-based APIs</th>
    </tr>
  </thead>
  <tbody>
    <tr>
        <td colspan="2" align="center"><a href="./docs/source/quantization.md">Quantization</a></td>
        <td colspan="2" align="center"><a href="./docs/source/mixed_precision.md">Advanced Mixed Precision</a></td>
        <td colspan="2" align="center"><a href="./docs/source/pruning.md">Pruning (Sparsity)</a></td>
        <td colspan="2" align="center"><a href="./docs/source/distillation.md">Distillation</a></td>
    </tr>
    <tr>
        <td colspan="2" align="center"><a href="./docs/source/orchestration.md">Orchestration</a></td>
        <td colspan="2" align="center"><a href="./docs/source/benchmark.md">Benchmarking</a></td>
        <td colspan="2" align="center"><a href="./docs/source/distributed.md">Distributed Compression</a></td>
        <td colspan="2" align="center"><a href="./docs/source/export.md">Model Export</a></td>
    </tr>
  </tbody>
  <thead>
    <tr>
      <th colspan="8">Neural Coder (Zero-code Optimization)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
        <td colspan="2" align="center"><a href="./neural_coder/docs/PythonLauncher.md">Launcher</a></td>
        <td colspan="2" align="center"><a href="./neural_coder/extensions/neural_compressor_ext_lab/README.md">JupyterLab Extension</a></td>
        <td colspan="2" align="center"><a href="./neural_coder/extensions/neural_compressor_ext_vscode/README.md">Visual Studio Code Extension</a></td>
        <td colspan="2" align="center"><a href="./neural_coder/docs/SupportMatrix.md">Supported Matrix</a></td>
    </tr>
  </tbody>
  <thead>
      <tr>
        <th colspan="8">Advanced Topics</th>
      </tr>
  </thead>
  <tbody>
      <tr>
          <td colspan="2" align="center"><a href="./docs/source/adaptor.md">Adaptor</a></td>
          <td colspan="2" align="center"><a href="./docs/source/tuning_strategies.md">Strategy</a></td>
          <td colspan="2" align="center"><a href="./docs/source/distillation_quantization.md">Distillation for Quantization</a></td>
          <td colspan="2" align="center"><a href="./docs/source/smooth_quant.md">SmoothQuant</td>
      </tr>
      <tr>
          <td colspan="4" align="center"><a href="./docs/source/quantization_weight_only.md">Weight-Only Quantization (INT8/INT4/FP4/NF4) </td>
          <td colspan="2" align="center"><a href="https://github.com/intel/neural-compressor/blob/fp8_adaptor/docs/source/fp8.md">FP8 Quantization </td>
          <td colspan="2" align="center"><a href="./docs/source/quantization_layer_wise.md">Layer-Wise Quantization </td>
      </tr>
  </tbody>
  <thead>
      <tr>
        <th colspan="8">Innovations for Productivity</th>
      </tr>
  </thead>
  <tbody>
      <tr>
          <td colspan="4" align="center"><a href="./neural_insights/README.md">Neural Insights</a></td>
          <td colspan="4" align="center"><a href="./neural_solution/README.md">Neural Solution</a></td>
      </tr>
  </tbody>
</table>

> [!NOTE] 
> More documentations can be found at [User Guide](https://github.com/intel/neural-compressor/blob/master/docs/source/user_guide.md).

## Selected Publications/Events
* Blog by Intel: [Effective Weight-Only Quantization for Large Language Models with Intel® Neural Compressor](https://community.intel.com/t5/Blogs/Tech-Innovation/Artificial-Intelligence-AI/Effective-Weight-Only-Quantization-for-Large-Language-Models/post/1529552) (Oct 2023)
* EMNLP'2023 (Under Review): [TEQ: Trainable Equivalent Transformation for Quantization of LLMs](https://openreview.net/forum?id=iaI8xEINAf&referrer=%5BAuthor%20Console%5D) (Sep 2023)
* arXiv: [Efficient Post-training Quantization with FP8 Formats](https://arxiv.org/abs/2309.14592) (Sep 2023)
* arXiv: [Optimize Weight Rounding via Signed Gradient Descent for the Quantization of LLMs](https://arxiv.org/abs/2309.05516) (Sep 2023)
* NeurIPS'2022: [Fast Distilbert on CPUs](https://arxiv.org/abs/2211.07715) (Oct 2022)
* NeurIPS'2022: [QuaLA-MiniLM: a Quantized Length Adaptive MiniLM](https://arxiv.org/abs/2210.17114) (Oct 2022)

> [!NOTE]
> View [Full Publication List](https://github.com/intel/neural-compressor/blob/master/docs/source/publication_list.md).

## Additional Content

* [Release Information](./docs/source/releases_info.md)
* [Contribution Guidelines](./docs/source/CONTRIBUTING.md)
* [Legal Information](./docs/source/legal_information.md)
* [Security Policy](SECURITY.md)

## Communication 
- [GitHub Issues](https://github.com/intel/neural-compressor/issues): mainly for bug reports, new feature requests, question asking, etc.
- [Email](mailto:inc.maintainers@intel.com): welcome to raise any interesting research ideas on model compression techniques by email for collaborations.  
- [Discord Channel](https://discord.com/invite/Wxk3J3ZJkU): join the discord channel for more flexible technical discussion.
- [WeChat group](/docs/source/imgs/wechat_group.jpg): scan the QA code to join the technical discussion.

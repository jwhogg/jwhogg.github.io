---
title: 'Edge AI: ML inference in the browser'
date: "2024-06-18"
draft: false
toc: false
math: false
readTime: true
tags: ["Machine Learning", "WebGPU", "Research"]
showTags: false
---

Recently, I stumbled across a [guy who ported](https://whisper.ggerganov.com/) OpenAI's [Whisper](https://github.com/openai/whisper) model into c++, in various sizes, allowing the model to be run on-device, at impressive speed.

{{< greycaption >}} [(source)](https://github.com/ggerganov/whisper.cpp) {{< /greycaption >}}
![whisper running on iphone](/images/whisper_iphone.gif#smaller)

I went down a rabbit-hole, and found a whole family of popular models that had been ported to work on-device, from the browser:
* [Stable difusion running in browser](https://websd.mlc.ai/#text-to-image-generation-demo)
* [Text emotion prediction in browser](https://github.com/jobergum/browser-ml-inference?tab=readme-ov-file)
* [Llama c++](https://github.com/ggerganov/llama.cpp)
* [Web LLM](https://webllm.mlc.ai/)
* [YOLO in the browser](https://hyuto.github.io/yolov5-onnxruntime-web/)

![yolo in the browser](/images/yolo_browser.png#small)

### Edge Computing
This movement is part of the larger [Edge computing](https://www.cloudflare.com/learning/serverless/glossary/what-is-edge-computing/) trend, which focuses on bringing computing as close to the source as possible, to reduce latency. The demand for edge AI will no doubt grow as consumers become more aware of the privacy issues with processing increasingly personal data in the cloud for their AI services. At [WWDC 24'](https://machinelearning.apple.com/research/introducing-apple-foundation-models), Apple put a focus on user privacy, and on-device intelligence- to make this possible we need much smaller models.

### WebGPU
Announced as the succesor to WebGL in 2021, WebGPU allows webpages to utilise a device's GPU, unlocking much more power for modern applications. Although only a handful of browsers support it currently (Chrome Canary, Firefox-latest), it promises to expedite the Edge AI movement.

WebGPU can be used with [WASM](https://webassembly.org/) (Web Assembly) for fast, high performance applications in the browser. WASM can be built from languages like C/C++, Rust and many others. Compiling ML models for WASM, we can acheive performance close to native GPU:

{{< greycaption >}} Using Apache TVM, [there isn't much loss vs running on GPU natively:](https://tvm.apache.org/2020/05/14/compiling-machine-learning-to-webassembly-and-webgpu) {{< /greycaption >}}
![webgpu performance is similar to native](/images/webgpu_comparison.png#smaller)

{{< greycaption >}} {{< /greycaption >}}

{{< notice tip >}}
Most browsers won't use WebGPU by default (see implementation status [here](https://github.com/gpuweb/gpuweb/wiki/Implementation-Status)), so to get the speedup it offers, you should use [Chrome Canary](https://www.google.com/intl/en_uk/chrome/canary/) or [Firefox Nightly](https://wiki.mozilla.org/Nightly) for the time being.
{{< /notice >}}

### Options for running models in the browser

##### 1- Tensorflow JS
The TensorFlow team have a JavaScript libary, that allows you to run pre-trained models in the browser using just pure JS, with relative ease. [Here's a great tutorial showing how to do this made by the team](https://www.youtube.com/watch?v=5QAO0mKFAKE)

Although TF-JS doesn't use the WebGPU backend by default, there are [options to support it](https://stackoverflow.com/questions/58112073/how-to-activate-webgpu-backend-on-tensorflow-js).

##### 2- ONNX Web Runtime
The team behind [ONNX](https://onnx.ai/), an open-soruce format for NN models, [leverage WASM and WebGPU](https://cloudblogs.microsoft.com/opensource/2021/09/02/onnx-runtime-web-running-your-machine-learning-model-in-browser/) to run models in any format (PyTorch, TF, ONNX) in the browser. See a great tutorial to build a Next.JS app for object classification with ONNX Web Runtime [here](https://onnxruntime.ai/docs/tutorials/web/classify-images-nextjs-github-template.html).

##### 3- Pure WASM + WebGPU
Using Rust or C/C++ bindings, it would be possible to implement ML models written in pure shader language, although this would quite hard, and not at all feasible for complex models.

The Apache TVM (a compiler for NN models) is making efforts to [support rust](https://github.com/apache/incubator-tvm/tree/master/rust), and there is the [ggml](https://github.com/ggerganov/ggml) ML libary, written in c. Rust also has a `wgpu` libary for working with WebGPU.

This technology is still in its infancy, but is very promising, and I'm excited to see where it goes.

#### Quick Example
Here's how you can get a quick example project up and running. Note that you should navigate to `localhost:3000/` on a supported browser to see the project.
```
git clone https://github.com/microsoft/onnxruntime-nextjs-template.git
cd onnxruntime-nextjs-template
export NODE_OPTIONS=--openssl-legacy-provider; npm run dev
```

### Sources / Further Reading:

[Rust+WebAssembly- Game of Life](https://wasm-game-of-life.shalzz.vercel.app/)
	(not web gpu but cool)
- [Tutorial on this here](https://rustwasm.github.io/book/game-of-life/hello-world.html)

[How to use webgpu to run a classification model](https://blog.logrocket.com/webgpu-accelerate-ml-workloads-browser/)

[WebGPU basics for AI](https://lablab.ai/tech/webgpu)

[WebGPU examples](https://webgpu.github.io/webgpu-samples/?sample=cornell)

[ML in shaders - shallow NN](https://darienbrito.com/2019/07/20/machine-learning-in-shaders-2-shallow-neural-network/)

[Good WebGPU typescript tutorial](https://alain.xyz/blog/raw-webgpu)

[WebGPU context and languages](https://cohost.org/mcc/post/1406157-i-want-to-talk-about-webgpu)

[Rust wgpu tutorial](https://sotrh.github.io/learn-wgpu/#why-rust)

[Text emotion prediction in browser](https://github.com/jobergum/browser-ml-inference?tab=readme-ov-file)

[ML inference on the edge](https://bergum.medium.com/moving-ml-inference-from-the-cloud-to-the-edge-d6f98dbdb2e3)

[Tutorial: Classifier using ONNX web runtime](https://onnxruntime.ai/docs/tutorials/web/classify-images-nextjs-github-template.html)

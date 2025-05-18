Implemented and pre-trained GPT from scratch, trained on wikipedia and some Shakespeare(ref Andrej Karpathy's [tutorial](https://www.youtube.com/watch?v=kCc8FmEb1nY)). Implementational details might differ.

<h3>Model Details</h3>
1. Model size: 71M parameters
2. Attention heads: 12
3. Number of decoders : 10
4. Embedding dim: 768

<h3>Tweaks</h3>:
1. Trained with DynamicTanh instead of LayerNorm and SwiGLU activation instead of ReLU as well. DyTanh is from a [2025 paper](https://arxiv.org/pdf/2503.10622) co-authored by Yann Lecunn, aims to reduce computational cost for maintained performance.
2. Implemented a parallelized version of SwiGLU that is 50% faster for embeddind size of 4096.
3. KV caching increasing speed on CPU(i7 12th gen) by 400% (for just 100 max_new_tokens) and 10-14% for GPU(RTX 3070 laptop)
4. Multihead Latent Attention(from Deepseek V2) as an option instead of Multihead Attention.


<h3>Training Details</h3>
1. Number of iterations = 100k
2. Batch size = 8
3. Val Loss = 1.16

Dataset used : [rahular/simple-wikipedia]([url](https://huggingface.co/datasets/rahular/simple-wikipedia))

<h3>Other Observations</h3>
1. Increasing VRAM freq by 700 MHz imoroved training speed by 10%, but stability is not guaranteed(loss went to NaN when overclocked by 800 MHz).
2. 

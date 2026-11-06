* Student: Aditya Kakarla (akakarla@ucsd.edu)
* Course: Quantization in ML Models
* Capstone Mentor: Arya Mazumdar (amazumdar@ucsd.edu)

**What is the most interesting topic covered in your domain this quarter?**

The most interesting topic covered thus far has been the research supporting KIVI quantization. Understading the "why" behind KIVI requires us to understand the patterns observed in key and value caches. For instance, the KIVI paper discusses a pattern in found in key caches - outliers tend to be aggregated in a select subset of columns. On the other hand, value caches tend to have outliers everywhere. This insight guides the development behind KIVI and why the authors chose to quantize key caches using per-channel quantization rather than per-token quantization.

**Describe a possible investigation you would like to pursue for your Quarter 2 Project.**

One possible investigation is looking into possible quantization methods for the value cache. The KV paper had discussed that the value cache has outliers often randomly distributed, but interestingly, while investigating our Quen model, we saw that this wasn't always the case. While there were definitely more random outliers compared to the key cache, there were still one or two channels that had extreme outlier values. That makes me wonder if per-token is the right quantization method for the value cache. Maybe there's possibly a better method that we should take a look at. I think that's something that would be quite interesting to pursue. 

**What is a potential change you'd make to the approach taken in your Quarter 1 Project?**

The only possible change would be exploring different models. We are currently testing Qwen3-1.7B for a variety of reasons, namely that it is a small model and that it is a text-only model. I wonder, though, how different models may have different patterns in their key and value caches, possibly corresponding to the attention layers/architecture utilized for that model. For instance, the Llama family of models may have a completely different architecture and thus possible key-value cache patterns than the Qwen family of models. 

**What other techniques would you be interested in using in your project?**

It would be interesting to think about the engineering possibilities as to how to implement the key quantization method. I think, as a whole, the idea of quantizing key caches per channel and value caches per token generally makes sense, but I wonder what possible differences we can introduce. For instance, as we were looking through prior work, we noticed that some papers argue that the most recent tokens are the most important, which generally seems to be true. A few others had mentioned that maintaining the first few tokens as well in a KV cache can be helpful for improving results and avoiding performance degradation. I wonder if we could possibly modify the KV implementation such that, instead of just keeping recent tokens in full value, maybe we can explore keeping both those and the first few tokens in the full value and not quantized.

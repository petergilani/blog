---
layout: post
title: PrivateGPT
---

This last week, I setup [PrivateGPT](https://github.com/imartinez/privateGPT) with [LlamaCpp](https://github.com/abetlen/llama-cpp-python):
[![GPUs]({{ site.baseurl }}/images/gpus.jpeg)]({{site.baseurl}}/privategpt)

PrivateGPT allows you to:
```"Ask questions to your documents without an internet connection, using the power of LLMs."```

There were a number of [issues](#issues) to work through, to get to the current functional state.

## Example

In this example, I downloaded several public resources, including the [RCG Product Deep Dive](https://www.rackspace.com/resources/ebook-rackconnect-global-product-deep-dive), into the ```'source_documents/'``` directory, which are then ingested, where the data is split into chunks and embeddings are created by your model of choice - currently I am using [all-mpnet-base-v2](https://huggingface.co/sentence-transformers/all-mpnet-base-v2) due to its quality [rating](https://www.sbert.net/docs/pretrained_models.html):

![RCG Deep Dive screenshot]({{ site.baseurl }}/images/rcg_product_deep_dive_screenshot.jpeg "RCG Deep Dive screenshot")

After the embeddings model has generated the new database, run the LLM (Large Language Model) against it to query the newly 'learnt' information. Currently I am using the [koala-7B.ggmlv3.q6_K.bin](https://huggingface.co/TheBloke/koala-7B-GGML) model - more info on Koala [here](https://bair.berkeley.edu/blog/2023/04/03/koala/):
[![RCG Deep Dive query]({{ site.baseurl }}/images/deep_dive_query.jpeg "RCG Deep Dive query")]({{ site.baseurl }}/images/deep_dive_query.jpeg)
*Click image to expand*

The above query is a rudimentary example, demonstrating the interpretive capability of understanding the context of which document, where in it, and what information to extract - based on the given question and documents provided. But the real value comes with the combination and interpretation of multiple sources.

## Accuracy
Astute readers may notice that while the answer is correct in terms of the two cloud providers identified, [OCI (Oracle Cloud Infrastructure)](https://docs.oracle.com/en-us/iaas/Content/home.htm) has not been referred to as OCP (Platform) for quite some time, making this an error that should be corrected.

The term is not found in any the documents I ingested, so is a limitation of the LLM's existing knowledge (which it states has a cutoff date of 2021-12-31) - so this is really something we would expect it to already know.

With the ability to ingest more documents and embed into our existing database, this is easily solved with a PDF of the [OCI User Guide](https://www.oracle.com/oce/dc/assets/CONT1B79FBD79BF543B18459A353101B0F91/native/oci-user-guide.pdf).

5,787 pages and 10 mins of embeddings later, our model has 'learnt' the specifics of Oracle Cloud.

Now, no matter how many times I repeat the question, it does not make the same mistake as before and correctly uses either Oracle Cloud Infrastructure, or just Oracle Cloud, every time:

> Answer (took 4.25 s.):
 In the first scenario for RCG for multicloud connectivity, a managed dedicated customer wants to establish private, high speed and low latency connectivity between AWS and **Oracle Cloud** via Partner Fabric.

> Answer (took 11.96 s.):
 When discussing RackConnect Global in the context of multicloud connectivity, both AWS and **Oracle Cloud Infrastructure** are used. The specific details of the connectivity between these two cloud providers will depend on the customer's requirements and implementation details.

## Performance and Monitoring
The result so far provides an impressive experience. Responses are accurate more often than not and returned in an acceptable time (~6-30s) using the combined compute power of my x3 NVIDIA GeForce GTX TITAN X GPUs. There seems to be potential to further tune performance as the individual GPUs are peaking around 60-70% compute, and different models may provide more accurate and improved responses.
![GPU Usage]({{ site.baseurl }}/images/gpu_usage.jpeg "GPU Usage")

As a side note, I have been using task manager for real time GPU usage, as opposed to Grafana, which has the 10s delay interval to Prometheus, which itself has 10s interval to Telegraf, which itself is polling individual metrics such as GPU usage at a 10s interval, meaning the most recent value in Grafana can be up to 20s behind depending on how the intervals overlap. So this got me thinking, why can't Grafana talk to Telegraf directly to facilitate a real-time dashboard for when the focus is current as opposed to historical usage? It turns out this was recently made [possible](https://grafana.com/tutorials/stream-metrics-from-telegraf-to-grafana/) which I plan to setup ASAP and cover in a future post.

**Update 13th Oct 23** - Telegraf -> Grafana realtime streaming working
![GPU Util Stream]({{ site.baseurl }}/images/gpu_util_stream.gif "GPU Util Stream")
![GPU Speed]({{ site.baseurl }}/images/gpu_speed.gif "GPU Speed")
The metrics now populate in the new live visualization dashboards within ~2s of being collected, which is realtime enough for me to happily ditch task manager. I will consider deploying a new Grafana instance on the same network subnet, or even the same machine as privateGPT, to see how much I can bring this number down.

## Issues
Expect to see another post on this topic - for now here are some of the setup issues I ran into:

 - [ERROR: Failed building wheel for llama-cpp-python](https://github.com/oobabooga/text-generation-webui/issues/1534)
 - [how can i use gpu to run?](https://github.com/imartinez/privateGPT/issues/79)
 - [llama-cpp-python now supports GPU, privateGPT a lot faster now](https://github.com/imartinez/privateGPT/issues/885)
 - [got the error: out of memory ,when invoke cuda in wsl2](https://github.com/microsoft/WSL/issues/8447)
 - [Failed to detect a default CUDA architecture](https://github.com/abetlen/llama-cpp-python/issues/627)

## Related
And here are some related links:

 - [LangChain - Run LLMs Locally](https://python.langchain.com/docs/guides/local_llms)
 - [GPT4All](https://gpt4all.io/)
 - [Llama 2 Announcement](https://ai.meta.com/blog/llama-2/)
 - [Llama 2 Research](https://ai.meta.com/research/publications/llama-2-open-foundation-and-fine-tuned-chat-models/)
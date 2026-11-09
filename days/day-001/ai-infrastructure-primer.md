# A primer on AI Infrastructure

> Original draft from Day 001 · November 6, 2026. The blog post was published on Substack on November 8, 2026; published link to come.

There’s an overwhelming number of new terms and concepts, and an influx of content. I’ve been increasingly interested in the state of AI, in topics such as software factories, model routing, and the infrastructure behind it all.

What I realized, though, is that I have some foundation, but I’m nowhere near where I want to be. And I think everyone (engineer or not) should have a basic understanding of what AI infrastructure looks like.

There’s immense value in understanding the concepts, and you can also just use them as your next dinner conversation. This is my effort to learn, and hopefully it will be helpful for others looking to learn more.

This post explains in plain English what happens after you send a prompt.

We’re looking at the part that runs a model to produce an answer, this is called inference. I’m going to use ChatGPT as the example to explain how this kind of system can work.

## 1. Model

First, the model and the application are two different things.

- **GPT:** a family of models from OpenAI. There are different models from different companies, such as Claude, Gemini, and Llama. A model is a big set of calculations, and it has weights which are the numbers learned from training.
- **ChatGPT:** the application wrapped around the model. It handles things like the chat interface, memory and conversation history. You’ll also hear this being called the harness.

Think of the flow of interacting with a model as:

**Input → model: calculations using the learned weights → output**

## 2. GPU and VRAM

Ok, so can we run the model on our own computer? We can run some models on our computers, including on CPUs, but the hard part is running a very large model quickly.

In a computer you have CPU and RAM:

- **CPU:** the processor — does the calculations.
- **RAM:** the working memory — holds the data the processor needs.

You said CPU, isn’t it GPU? Yes. A model does a lot of calculations, and many of them can run in parallel. CPUs are not designed for that. GPUs are designed for this, they can run similar calculations in parallel. That’s what makes them useful for running large models.

Another problem that makes computers not ideal is the memory.

A GPU on the other hand has its own memory, called VRAM. It sits on the card or alongside the GPU, with a fast connection that lets the GPU read a lot of data very quickly. The memory is a very important consideration as it’s limited to the VRAM.

So on a chip now you have:

- **GPU:** the processor
- **VRAM:** the memory

## 3. Compute, bandwidth, memory

So the way to look at a GPU is to look at 3 things:

1. **Compute:** how much calculation it can do per second, measured in FLOPS.
2. **Bandwidth:** how much data can move between memory and the processor per second, measured in GB/s or TB/s.
3. **Memory capacity:** how much data it can hold, measured in GB.

You need to consider the best GPU for the task. Similar to how you’d look at a computer.

## 4. PyTorch and vLLM

Okay, so we talked about the chip that runs the model. There also needs to be software, because the GPU can’t do stuff on its own.

PyTorch is a software framework for building and running models.

You need a service around that.

Enter: vLLM, it’s an engine for running and serving language models. It uses PyTorch and can run as a service that stays on, gets requests, and sends answers back.

So the next question: what does the server actually do when a request comes in?

Here it’s important to understand what tokens are. You surely have heard of them, and probably been limited by them.

An LLM (large language model) doesn’t read and write like we do. The text is cut into little pieces called tokens. A token can be a whole word or just part of a word.

These pieces are represented as numbers for the model to process. The model generates tokens, which are then also turned back into the text for you to see.

Requests can be very different.

You might ask, “Can you summarize my rent contract?” That’s a short question, but the model also needs the text from the contract.

All of that makes up the input tokens. The answer the model generates is made up of output tokens.

Okay, so there are two parts to this: processing the input and generating the answer. That’s where prefill and decode come in.

## 5. Prefill and decode

Okay, so your request has been turned into input tokens. The model now needs to process those tokens and generate output tokens, which is your answer.

There are two main parts to this process:

- **Prefill:** processing the input tokens
- **Decode:** generating the output tokens.

Let’s say you’ve asked the model to summarize a document. It first processes the input tokens from your question and the document. This is the prefill stage.

The model then continues to create the answer. It uses the input and what it has already written to predict what could come next.

These output tokens are turned back into text and sent to the app. That’s why you see the summary appearing one-by-one on your screen. This is the decode stage.

During prefill, the model processes your input tokens. vLLM stores some of the results in a KV cache, usually in the GPU’s memory, or VRAM.

So when the model is writing your document summary, it can reuse that saved information. This saves work and helps it generate the answer faster.

But that saved work takes up space too. Remember the limited GPU memory? It needs room for both the model’s weights and the caches for the requests being processed.

The serving software can also keep some cached results for later requests. For example, if you ask another question about the same document, it may be able to reuse work on the unchanged beginning of the input.

## 6. Routing and llm-d

Okay, so we have the model running, and we’re saving some of the work in a cache. But what happens when lots of people are sending prompts at the same time?

To handle lots of requests, the company serving the model can run copies of it across multiple servers. Its routing system then decides where each request goes.

Typically, a load balancer distributes incoming requests across servers.

But this gets more complicated with LLMs. A short question and a long contract don’t create the same amount of work. And one server might already have useful work cached for your prompt.

That’s one of the problems llm-d helps with. It’s an open-source project launched by companies including Red Hat, Google Cloud, and NVIDIA. It helps coordinate model servers such as vLLM across a fleet of machines.

When deciding where to send a request, it can consider:

- **Saved work:** does a server already have a useful part of this prompt cached?
- **Memory:** how much of its KV-cache space is already being used?
- **Load:** how many requests are running or waiting?

For example, if you ask another question about the same contract, sending it to a server that has the beginning of the input cached could save work. But if that server is very busy, another server could still get you an answer faster.

Here we’re choosing which server handles your request. Choosing which model to use is another kind of routing.

## How it all comes together

Okay, so let’s put this together. You open ChatGPT and ask: “Can you give me an easy lasagna recipe?”

Here’s a simplified version of what happens.

1. The app prepares the input for the model. That includes your question, any additional context, and relevant conversation history. So if you said earlier in the chat that you’re vegetarian, that can be included too.
2. Behind the scenes, the software directs the request to the hardware running the model and prepares the input as tokens. In a typical setup, the model’s weights are already loaded into GPU memory, ready to be used.
3. During prefill, the model processes that input: you want an easy lasagna recipe, and you’ve said you’re vegetarian. Some of the calculations are saved in the KV cache, so they can be reused as the answer is generated.
4. Then comes decode. The model uses the input to predict what could come next. A token is selected, added to the response, and the process repeats, taking into account what it has already written. This is how the recipe is generated, step by step.
5. The tokens that make up the answer are turned back into text and streamed to the app. On your screen, you start seeing the ingredients and cooking instructions appear.

And that’s how it all comes together.

This is just the part of AI infrastructure that serves the model. We haven’t gone into how the models are built or trained. But I think it’s useful to have a basic picture of the infrastructure, and it’s pretty cool to visualize all of this in your head when you send a prompt to ChatGPT.


# Questions

## .

## Only general language LLM

How do you train an LLM so it learns basic english but doesn't learn any specific knowledge?

For example, if you train an LLM on a training set that includes some text like: "The capital city of the USA is Washington DC", it'll most likely learn that information specifically because training is encouraging it to reproduce that it specifically

One solution idea is to lossily encode (via learned encoder) both the output of the LLM and the training output and compare the encoded values. For instance, if you trained an encoder to compress the same kind of words (noun, verb, etc) to the same value, then the network would learn to produce the correct next *type* of word

## IDK LLM

How do you train an LLM to say "I don't know" if it can't actually produce the correct output without confabulation and hallucination?

Solution idea: RLHF (for normal speaking) and tree of thought?

Another solution idea: look at training examples with high losses (or another metric?) and exclude them from training. Similarly: during training, use a loss function that is zero after some point somehow to discourage learning expensive-to-learn things

## How do you make ANNs more resource efficient? (Open ended)?

For instance: smaller, faster, etc

## Is it true that the more losses the better when training an ANN?

Relevant: see the `Equivalence between training, test sets and equation solving` idea below

The more information you can provide about the problem you want to solve, the better; and you can only provide information via losses (roughly speaking)

## How do you make a ML model use analogy?

Analogy is like some partial similarity between two structures. ie: There is a equivalence relation between some elements in two structures

Humans probably encode

## How do you train an LLM which searches?

If `X' = p(X, s(q(X)))` where `p` predicts the next token from the original input and a result object, `s` is a non-differentiable search function that returns result objects, and `q` is a query-making function. Ideally, `s` is actually searching a database. Since `s` isn't differentiable, you can't backprop through it. So how do you train `s`?

## In LLMs, does presenting facts on input during training prevent learning of those facts?

For example: "The dog's name is Walter. [...]. Bla bla. The dog's name is " and the model is trained to complete the text with : "Walter". But it doesn't need to have encoded that response parametrically because its presented on input

# Ideas

I'm going to try to make an effort to write down my machine learning and AI ideas here

## Image correction ML model

Think: Stable Diffusion makes *almost* correct images, this model would go through and fix small details

## Warp diffusion

This is like a generative image diffusion model, but uses warp noise (randomly warped image) instead of additive noise

## Language / code correction LLM

An LLM that takes some code or general language that's been corrupted somehow (eg: replace random characters, words; swap words, etc) and it rebuilds the un-corrupted version

## Unit vector training

For the output of a softmax `v`, you can include `1 - max(v)` as a loss to encourage the softmax vector to unitize (turn into a unit vector)

I've tested this, and it works. But I'm still not sure if it always converges to the optimal unit vector

## Random initialization hyperparameter optimization

For a network like $f(x; p, q)$ with some hyperparameter $q$, sum up the gradients for random io pairs wrt $q$ for multiple random initializations of $p$. The point is to find a $q$ that optimizes the function's architecture over random parameter values

## Equivalence between training, test sets and equation solving

For some network $f$ where you want to find parameters $p$ that make $f(x; p) = y$ for $(x, y) \in T$ where $T$ is the training set, you also want this to be true for $(x, y) \in T^\prime$ where $T^\prime$ is the test set. However, this is exactly equivalent to when you solve equations in typical mathematics

So the question is: how do you solve a system of equations $f(x; p) = y$ for $p$ when you given $n$ equations but want the solution to be valid for $N > n$ equations? ie: You want to solve it for all the equations but don't know some of the equations

Ideas:
* You probably need prior knowledge to model the equations, so you can predict what the not-given equations are
* Any constraints $g(x, y; p) = 0$ you know are valid for all solutions will help (in ANN training terms: more losses are probably better)

## Optimizer agents

Use an agent to optimize a system, rather than use gradient descent, or other techniques

## Understanding vs knowledge

Understanding and knowledge seem to lie on a continuum, where understanding is the equivalent of deep, highly-encoded, parametric knowledge, and knowledge is the equivalent of shallow, single-step understanding

In a sense, understanding is generalized knowledge: knowledge that applies to lots of different situations

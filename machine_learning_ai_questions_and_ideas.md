
# Questions

## .

## Only general language LLM

How do you train an LLM so it learns basic english but doesn't learn any specific knowledge?

For example, if you train an LLM on a training set that includes some text like: "The capital city of the USA is Washington DC", it'll most likely learn that information specifically because training is encouraging it to reproduce that it specifically

One solution idea is to lossily encode (via learned encoder) both the output of the LLM and the training output and compare the encoded values. For instance, if you trained an encoder to compress the same kind of words (noun, verb, etc) to the same value, then the network would learn to produce the correct next *type* of word

## IDK LLM

How do you train an LLM to say "I don't know" if it can't actually produce the correct output without confabulation and hallucination?

Solution idea: RLHF (for normal speaking) and tree of thought?

## How do you make ANNs more resource efficient? (Open ended)

For instance: smaller, faster, etc


# Ideas

I'm going to try to make an effort to write down my machine learning and AI ideas here

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


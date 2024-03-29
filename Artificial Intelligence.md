# Artificial Intelligence


### Neural Compositional Denotational Semantics for Question Answering

Topic : Deep Learning, Natural Language Processing, Computational Linguistics

<https://arxiv.org/pdf/1808.09942.pdf>

One of main challengge in computational linguistics is query and answering, given knowledge graph.
In specific, knowledge graph is given as n items, properties of item, relations between item.
Then the goal is to give correct answer for natural language question.
This paper neural compositional denotational semantics, which is combination of ML-based NLP and
computational linguistics based NLP.
First, every span of text are assigned to type, like E(entity), T(Truth), R(Relation), phi(vacuous).
And their embedding is defined by their type, as entity to n-length vector, relation to n times n matrix.
For each syntax rule, like E(Large) + E(Red) -> E(Large Red), we define rule to compose each embedding
of types. 
Then this model is trained, where trained vector is embedding of each word, and probability of type for each word.
In result, this model shows 100% correctness for short questions, and 84.6% correctness for complex question.

### An Inductive Synthesis Framework for Verifiable Reinforcement Learning

Topic : Reinforcement Learning, Program Verification

<https://herowanzhu.github.io/herowanzhu.github.io/pldi2019.pdf>

There are consecutive researches on verification of neural network, which is complex due to nonlinearity and
stochasticity of neural network.
This paper focuses on verifying reinforcement learning on low number of variable.
First it generates deterministic, relatively simple function that approximates neural network,
and find some invariant that assures this simple function is safe.
Now to lift safety proof to neural network, if neural network violates invariant, we use function's action
instead of neural network.
In finding deterministic function and constraint, it first finds some initial point not-currently-covered, and tries to find
neighborhood of that point which is consistent under deterministic function by reducing radius.
Then if whole initial space is covered with such covers, conditional combination of deterministic function becomes resulting function.

### Code2Vec: Learning Distributed Representations of Code, Code2Seq: Generating Sequences From Structured Representations of Code

Topic : Embedding, Programming Language

<https://arxiv.org/pdf/1803.09473.pdf> <https://arxiv.org/pdf/1808.01400.pdf>

These two consecutive models is new neural network model on programming language, which is highly structured.
The basic principle is viewing code as a AST(Abstract Syntax Tree), and input as path between terminal nodes.
In Code2Vec, each unique terminal and paths are embedded to d-dimensional vector. Now for each path and its two ends,
embed it to d-dimensional vector with FC layer, and finally multiplying attention value gives resulting representation.
In Code2Seq, each terminal is decomposed to subterminals, as ArrayList to Array + List, and representation is summed up.
The path is encoded by LSTM to single d-dimensional vector.
Now concatenate two ends and path, embed to d-dimensional vector with FC-layer, and multiplying attention, finally decoder network
generates target sequence.

### Learning Nonlinear Loop Invariants with Gated Continuous Logic Networks

Topic : Logic Learning, Programming Language

<https://arxiv.org/pdf/2003.07959.pdf>

One of main undecidability in Program Logic is Loop Invariant, because we need to search for many formulas especially when invariant is nonlinear.
This paper proposes differentiable programming approach on loop invariant finding, with gated continuous logic network.
The basic idea relies on fuzzy logic, which is viewing a logic as a differentiable function satisfying some conditions, like T-norm and T-conorm.
To successfully find conjunction/disjunctions, the paper uses gated T-norm, which is continuous variation of conjunction and T-conorm.
And to find tight bound the formula uses new activation function which penalizes when term is too large (not tight).
Since convergence is not assured due to less test datas, the formula generalizes tests by using different initial value.
Also to encourage simplicity of formula and learning procedure, we use term dropout which is exhibiting some terms before training.
Final structure forms as CNF form, with two layer representing equality and inequality.
Then from learned fuzzy-logic formula, we extract discrete formula, and after rounding it, test with theorem prover. If there is counterexample,
add it as data and train again.
The proposed model resulted 26/27 correctness, with 97.5% convergence rate on quadratic problem.

### AI2: Safety and Robustness Certification of Neural Networks with Abstract Interpretation

Topic : Neural Network Robustness

<https://www.cs.rice.edu/~sc40/pubs/ai2.pdf>

Recently, adversarial examples are considered as significant threat on deep learning.
However due to complex structure of neural network, it is hard to prove some properties, like robustness.
This paper gives abstract interpretation for neural network, including MLP and CNN, that is able to prove robustness.
In specific, this paper treats four abstract interpretation, box, zonotope, polyhedra, union of N zonotopes.
First, we approximate given robustness condition by one of abstract interpretation.
Then, by viewing each layers like ReLU, FC, Conv, MaxPool as conditional affine transformation, 
where conditional is approximated with meet(abstract notion for intersection) and join(same for union).
Then finally, assuming that condition is given as conjunctions of inequalities, it checks whether meet of condition and abstract
interpretation is empty. If so, robustness is proved.
The paper runned robustness check on two dataset, MNIST and CIFAR10, with box, zonotope, polyhedra, zonotope2\~zonotope128,
where box showed bad result, polyhedra had extreme runtime, and zonotope/zonotope2\~zonotope128 worked well.
Also in comparison with Reluplex, this algorithm was much stronger in large sized neural net.

### Learning Differentiable Programs with Admissible Neural Heuristics

Topic : Program Learning

<https://arxiv.org/pdf/2007.12101.pdf>

Differentiable langauge is one of domain-specific language that is enable to optimize its parameters to approximate data.
However determining structure of program is complex, since it has exponentially many samples with respect to depth.
This paper proposes algorithm called NEAR, which extends A* algorithm by adding neural heuristics.
First, the DSL is given by regular language rules, and the search space is given by graph with each node as program structure,
and each edge as generation rule. The node is terminal if it has no nonterminal.
Then we perform A* algorithm from initial node which is empty structure. Here the cost is defined as minimum of loss of subprograms,
where loss is defined as sum of structural loss and data loss.
However this cost is intractable, so instead we use neural heuristics to approximate this cost. This heuristic will be epsilon-admissible.
Instead of rule, we replace each nonterminal as either one of RNN and MLP, preserving type, and loss of this program will be heuristic function.
Another algorithm proposed uses branch-and-bound instead of A* algorithm.
Comparison is done with four algorithms, simple graph search, monte carlo sampling, monte carlo tree search, and genetic algorithm. 

### Typilus: Neural Type Hints

Topic : Neural Type Inference

<https://arxiv.org/abs/2004.10657>

Type inference is one of well known task in programming language, where classical approaches fails from undecidability.
As an alternative, neural type inference are recently developed and used as probabilistic type suggestion.
This paper proposes Typilus, which allows adaptive type prediction unlike other previous research.
The usual loss used in neural type inference is classification loss, where the output is interpreted as probability of assigning each type.
However, this loss fails when the model is given new types that were not in dataset.
Instead, Typilus uses triple loss, and learns embedding to TypeSpace, while optimizing metric.
And to enhance the performance, instead of classical triple loss, Typilus extends it to mini-batch. In specific, it uses sum of classification loss and metric loss.
For the neural network model, the model uses Gated Graph Neural Network, which is given a graph with directed, labelled edges, returns feature with nodes.
Each neighbor nodes's feature is first transformed with single linear layer, and max pooled to single vector. Then viewing this as input vector and
feature of node as previous hidden state, we apply GRU cell. 
Now the input graph has four kinds of nodes, token, nonterminal, symbol, vocabulary.
Token is any lexical tokens, nonterminal is nonterminal in AST of program, symbol is each variable or function name, and finally vocabulary is subtoken of each symbol.
Then the edges are defined with selected labels, like next-token, next-possible-use, return-to. 
In inference task, we apply neural network to code graph, then each types are defined by using kNN in the TypeSpace.

### Neural Operator: Graph Kernel Network for Partial Differential Equations

Topic : Neural PDE solver

<https://arxiv.org/abs/2003.03485>

Partial differential equations are well used in many fields of engineering. Most of solution of PDEs are solved using numerical methods.
However numerical methods are slow, and is not re-usable, meaning that we need to solve it again if we face new PDE.
To resolve this problem, neural network based solver was proposed. But there were two main problems in previous researches.
First, they were not mesh-independent, meaning that the solution depends on level of discretization a lot.
The other problem is that those achieving mesh independency needs to learn PDE again if it face new PDE.
This paper uses two ideas to achieve this two problems.
First, using Green's function and representing solution with Green's function, it derives iterative approximation of solution.
Second, the integral inside the iterative approximation is implemented with graph neural network, where nodes are grid points,
and edges exists when two nodes have distance less than threshold. This idea makes this solution mesh-independent.

### Inference Compilation and Universal Probabilistic Programming

Topic : Probabilistic Inference Compilation

<https://arxiv.org/pdf/1610.09900.pdf>

Probabilistic Inference is one of major topic in machine learning, where we tries to find posterior distribution and expectation
from prior and observations. Probabilistic Programming Languages gives universal inference on these tasks, however they are not
fast enough. This paper gives neural network based inference compilation on these universal probabilistic programming.
First, we assume variable length of sampling and fixed length of observation. Each sampling is indexed by its address, instance,
and the sampled value. Observation is domain specifically defined, for example Captcha image. 
Then the neural network is RNN-like structure, first given the embedding of observations, input sequence is given by one hot encoding of
address and instance, and previous sampled value. The output is defined by proposal, which will approximate posterior distribution.
This architecture successfully solved two main problems, mixture model and Captcha problem where classical methods recently started to worked with.

### InferCode: Self-Supervised Learning of Code Representations by Predicting Subtrees

Topic : Embedding, Programming Language

Creating a universal representation for some data structure is important, so that we can handler multiple tasks in once.
Code2Seq has designed an universal representation for generating sequence from program, however some research have shown that the representation does not perform well on other tasks.
This paper uses self-supervised learning on program data, in particular treating its subtree as label.
The basic idea comes from Doc2Vec, which creates representation of document, by predicting words appearing in document.
First we first create node embedding using TBCNN, where initial value comes from each node's type and token information.
Then we aggregate the embedding of whole tree using attention mechanism.
For subtrees, we only use expr\_stmt, decl\_stmt, expr, condition, and learn each subtree's embedding.
Finally the predicted distribution is defined by softmax of inner products. 
The resulting model showed higher performance on five tasks, Code clustering, Code clone detection, Cross language code-to-code search.

### Improved Semantic Representations From Tree-Structured Long Short-Term Memory Networks

Topic : Natural Language Processing

<https://arxiv.org/abs/1503.00075>

In classical NLP approach, sentences are parsed to syntactic structure, and it has shown good performance in entity recognition, coreference.
After deep learning have introduced, most of networks views natural languages as hot-encoded sequence, which does not benefit from this syntactic structure.
In this paper, the author proposes new structure called TreeLSTM, that are able to process tree structured inputs. 
The base idea is simple, extending the LSTM network's structure so that it can receive multiple cell states and hidden states.
To handle this, the paper suggests two variants, child sum and k-ary. Child sum add up all the hidden states to single hidden state to handle
multiple state problem. In contrast, k-ary TreeLSTM uses k linear networks, requiring the tree becoming at most k-ary.
Child sum TreeLSTM is called dependency TreeLSTM since it is suitable to dependency tree, and binary TreeLSTM is called Constituency TreeLSTM since it is
well applied to binary constituency tree.
For the experiment, the paper tested this network to sentiment classification and semantic relation tasks.
For the sentiment classification, constituency TreeLSTM shown best result compared to LSTM, BiLSTM, and other models.
Conversely for the semantic relation task, dependency TreeLSTM shown best result.

### Understanding Neural Networks Through Deep Visualization

Topic : Interpretable AI

<https://arxiv.org/abs/1506.06579>

Though deep neural networks shown amazing results in various fields, however reason for their performance is not well understood.
This paper uses white box method to understand neural network's interpretation by visualizing each node as an image.
First visualization method is simple. Since every layer's channel can be viewed as grayscale image, simply visualize all channels for each layers.
With this visualization, the author could found channel that corresponds to face. 
Second visualization is slightly complicated, the basic idea is applying gradient ascent to image.
The seed is generated by averaging every training images. 
Then choose single neuron in network, then apply gradient ascent to the seed to maximize that neuron's activation value. 
However during gradient ascent, regularization is applied. There are four kinds of regularization, L2 decay, gaussian blur, pixel clipping with small norm or contributions.
With this method, the paper shows that each neurons learn specific features of image.

### Learning Imbalanced Datasets with Label-Distribution-Aware Margin Loss

Topic : Imbalanced Dataset Problem

<https://proceedings.neurips.cc/paper/2019/file/621461af90cadfdaf0e8d4cc25129f91-Paper.pdf>

Most of natural datasets are imbalanced, since many of distributions are long-tailed.
But in such datasets, neural network performs poorly on classes with less data, and this leads to ethical problems like fairness issue.
This paper proposes margin loss based solution, with theoretical backing.
The core idea of this paper is increasing classification margin for classes with less instances.
In algorithmic learning theory, imbalanced test error is bounded by some formula depending on number of data and margin length.
And this inequality shows that, increasing the margin makes the model to generalize well. 
Now, based on this observation, since our margin should be maximal among other choices of margin, we can derive correct value of margin.
Finally using Hinge Loss or cross entropy loss on margins gives resulting loss. 
Resampling and reweighting was not effective, however to utilize them, the paper uses different scheduling,
that they use resampling and rescheduling after enough training.

### Edge-Labeling Graph Neural Network for Few-shot Learning

Topic : Few-shot learning

<https://slsp.kaist.ac.kr/wiki/images/9/9a/6340.pdf>

Few shot learning is a problem with small dataset, in specific N-way K-shot problem has K data for each N classes, and should classify T test data.
This paper uses graph neural network to solve this problem, where each node represents data given, and each edge represents relation of two data.
First, each vector for nodes are initialized as embedding of given data, and each edge has two real number, 
where if two data has same class it is initialized as (1, 0), (0, 1) if different class, otherwise (0.5, 0.5).
Then each node vectors and edge values are updated by message passing from weighted sum of same classes and different classes.
After the update is done, prediction is done with softmaxing the similarity edge values with training datas. 

### Provable repair of deep neural networks

Topic : Neural Network Repair

<https://dl.acm.org/doi/10.1145/3453483.3454064>

Neural Networks often fails to output correct value, however repairing the network is infeasible due to its complex behavior.
Approaches before this paper used fine tuning, meaning that they retrain the network with wrong examples, however it usually fails and takes long time.
This paper proposes novel structure of neural network that enables polynomial time repair of network, using the linear programming. 
Preceding research had attempted similar proposal, however it takes exponential time, when solving the inequality.
The problem here is that, changing weights make both linear regions and linear functions change, since they are coupled.
So this paper proposes Decoupled DNN, where it simply uses two copy of layer, one for activation, one for real value. 
Then the repair becomes simple linear programming problem, since it is enough to consider layer dealing with value. 
Now since every region is linear, repair for polytope becomes simple, by repairing the vertices only.
As a result, the algorithm shows high performance compared to fine tuning.

### Fast and Precise Certification of Transformers

Topic : Neural Network Verification, Seq2Seq

<https://files.sri.inf.ethz.ch/website/papers/pldi21-transformers.pdf>

Abstract Interpretation based neural network verification have shown good result in MLP and CNN networks, however they lack their availiability to be applied in state-of-the-art architectures.
This paper proposes abstract interpretation based verification for state-of-the-art natural language processing network, transformer model.
Similar to preceding researches, this paper tries to verify robustness of model, that perturbation in sequence using synonyms does not change the output.
This paper also uses zonotope as abstract interpretation, however since perturbations is usually bounded by L1 norm or L2 norm, this paper defines Multi-norm zonotope which has noise bounded by L1 or L2 norm.
For the affine layers like addition, subtraction, and constant multiplication, abstract transformer is canonically defined.
For the activation layers like ReLU and Tanh, this paper extends preceding results to multi-norm case.
Now the problem happens in dot product layer which is used in self-attention layer, since it requires multiplication of two zonotopes.
This paper solves this problem by giving two solutions, fast solution using norm's bound, precise solution that contains all pairs of noises.
Now to optimize the result, this paper applies noise symbol reduction, which heuristically eliminate noise symbols to reduce computation time.
Also though exponential and reciprocal's abstract transformer is defined, softmax itself is redefined to assure that output's sum is one, and to use numerically stable version.


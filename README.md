
# ML Paper Checklist

I read a lot of ML papers. Sadly, a many seem to omit very useful information. Having tried to write some paper-like things myself, I actually don't think this is malicious -- it's very easy to forget some key details when you get into the meat of working on something complex.

As an aid to myself (and hopefully others), here is a list of things that I would like to know from every paper. Note that "code" is there at the bottom, but at some level, the goal of this list is to achieve reproducibility without the need to release the code. The full set of details here is very probably unsuitable for the main body of a work, but would always be nice in an appendix.

The list is (badly) organised by topic. I'm hoping that I'll add things as they occur to me, and that smart people will create pull requests), and generally turn it into less of an "off the top of my head" mess.

 - General:
     - [ ] You have presented some equations; some of which have scalar hyperparameters in them. Have you enumerated them for yourself and clearly specified the value or schedule of each of them?


 - Dataset
    - [ ] How many examples in the training/validation/test set?
    - [ ] Is the dataset publicly available?
    - [ ] What is the estimated human ceiling?
    - [ ] What is the estimated label noise?
    - [ ] How were the final figures selected?
        - [ ] Quoted for validation or test set?
        - [ ] Multiple training runs?
        - [ ] Which of Best/Worst/Mean/Median performance is quoted?
        - [ ] Ensemble used?
        - [ ] Confidence intervals over multiple training runs? (Look, GPU time is not cheap; just explicitly say if you couldn't do this)   
    - [ ] How were the comparison stats selected? (Copied from a paper or re-implemented? Did you exclude any similar-but-not-quite-comparable famous results?)
  
 - Classification Tasks:
     - [ ] Distribution of examples per class (# for each class, largest/smallest)
     - [ ] Baseline performance (pick randomly)
      - [ ] Baseline performance (pick mode)

 - Regression Tasks:
    - [ ] Distribution of regression target
    - [ ] Baseline performance (mean / median; also  linear / robust regression)
    - [ ] What loss was used? Huber/MAE/MSE/something custom. If it has a parameters, what were they (eg Huber margin)

 - Multi-task:
    - [ ] How were the task coefficients selected?
    - [ ] How much tuning of the task coefficients was needed?
    - [ ] Do you have an estimate of relative task difficulty?

 - Metric / Representation Learning
    - [ ] Performance on "raw" nn features from appropriate transfer task (eg imagenet CNN).

 - Active Learning:
    - [ ] Random selection baseline
    - [ ] Selection cost in asymptotic and real terms

 - Reinforcement Learning:
    - This is a whole 'nother kettle of fish. Perhaps with some external help, I could develop a similar checklist, plainly some of this stuff applies.

 - Tips+Tricks (There are too many of these to be really helpful, but to help stir the memory)
    - A curriculum?
    - Up-sampling tricks, or other sampling biases?
    - Label smoothing?
    - Sequence reversal?

- Data augmentation:
  - [ ] Did you do it?
  - [ ] What hyper-parameters?
  - [ ] Did it actually help? (eg ablate if possible)

 - Optimizer:
     - [ ] What stopping criteria was used?
     - [ ]  Optimizer (AMSGrad / SGD / ...)
     - [ ] Optimizer hyperparameters (learning rate, momentum, ... ; also how they were picked, even if they were picked badly)
    - [ ] Optimizer hyperparameter schedules, *and how they were picked; be honest*
    - Multi-Machine:
        - [ ] What is the synchronisation paradigm?
        - [ ] Was multi-machine necessary?
    


- Architectural Choices:

  - What is the exact architecture used? 
    - [ ] Number of layers
    - [ ] size of each layer (#params)
    - [ ] output shape of each layer
    - [ ] activation function of each layer; associated hyper-parameters
    - [ ] batch norm (before or after activation?, what hyper-parameters?)
    - [ ] initialisation scheme and hyper-parameters

  - If transfer learning used; what was the performance of random init?

  - For each proposed module; can you ablate to determine performance gain without it *or* by fixing its parameters if it cannot be excluded?
      
- Claims of Sota:
  - [ ] Is it just because your backbone CNN/RNN is better?
  - [ ] Is it just because your "tips+tricks" are better (see "The best of both worlds" machine translation for an example of this)
  - [ ] Is it just because your hyperparameter choices are better?
  - [ ] Is it just because your model is a mega-phat ensemble enormous comically deep O(2^n) insane "Netflix challenge" / kaggle monster? (See "performance characteristics")

- Performance Characteristics:
    - Theoretical:
        - [ ] Training - if we applied the best data structure at every point, what does the training cost look like compared to similar systems?
        - [ ] Same for Inference, theoretically
        - [ ] Theoretical memory costs of training/inference.

  - As Implemented:
      - Training:
          - [ ] CPU/GPU make/model/stats
          - [ ] main memory footprint (from htop; not the theoretical one)
          - [ ] GPU memory footprint (from nividia-smi, not the theoretical one)
          - [ ] MACs/FLOPs for forward/backward pass
          - [ ] Asymptotic training cost if it's not obvious.
          - [ ] wall clock time to training end (not until selected model)
          - [ ] examples seen to training end (not until selected model)
      -  Inference:
          - [ ] main memory footprint
          - [ ] gpu memory footprint
          - [ ] MACs/FLOPs for inference as tested (eg, if the test figures show a 10 crop ensemble; don't quote one forward pass)
          - [ ] Wall clock for inference as tested.
          - [ ]  Asymptotic cost for implemented inference scheme, if it's not obvious.

- Safety:
  - [ ] Any bias problems? Any de-biasing?

- [ ] Any code at all?

- [ ] Fully reproducible "just run this command to replicate the paper's tables" code?


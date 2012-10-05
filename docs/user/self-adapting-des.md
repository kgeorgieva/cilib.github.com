---
layout: docs
title: "Self-Adapting Differential Evolution"
description: ""
group: "user-docs"
tags: [code, master, changes, Differential evolution, de, self-adapting]
---
{% include JB/setup %}

This describes the self-adapting DE described by A. K. Qin and P. N. Suganthan in their 2005 IEEE
paper "Self-adaptive Differential Evolution Algorithm for Numerical Optimization". Their Self-adaptive 
DE consists of two parts. The first part is a probability based selection between two learning 
strategies. This selection process adapts the probability of a learning strategy to be chosen using 
information about the results of previous selections. The second part deals with the adaptation of the 
parameters themselves. Here the scaling factor parameter is randomly initialised but not adapted through 
time, while the crossover probability is randomly initialized and adapted according to a learning 
experience gathered during a set number of iterations.

# Available Algorithm Configurations
- Self Adaptive Differetial Evolution: This currently consists of a new iteration strategy that adapts the
scaling factor and crossover probability parameters (which are held by an individual) in parallel to the 
problem's solution.

# Implementation Details

- SaDECreationStrategy: This is a trial vector creation strategy which uses an adapting probability to 
choose one of two creation strategies that will be used to generate a trial vector for a particular 
individual. At first there is an equal probability to choose both strategies. As time passes, the 
probability is adapted depending on the total number of offspring surviving to the next generation, 
making the more successful creation strategy more likely to be chosen.

- SettableControlParameter: This is an interface that extends ContolParameter to allow for parameters
to be set and updated during the execution of the algorithm.

- StandardUpdatableControlParameter: This is a new control parameter that implements the SettableControlParameter
and allows for the parameter it holds to be, both, set and updated during the execution of the algorithm.

- ParameterAdaptationStrategy: This is an interface for new parameter adaptation strategies. It requires for 
strategies to have the methods change and accepted. Change which changes the parameter accordingly and accepted which
informs the adaptation strategy whether the offspring created with this parameter was successful.

- SaDEParameterAdaptationStrategy: This is a parameter adaptation strategy which adapts parameters according to the
method described by Qin and Sugathan in their 2005 paper  "Self-adaptive Differential Evolution Algorithm for Numerical
Optimization". Here the parameter is sampled from a gaussian distribution with a mean value that is adapted exery X 
iterations.

- ControlParameterInitialisationStrategy: This is an interface for initializationStrategies specific to control 
parameters. It requires for initialisation strategies for control parameters to have a getClone and initialize method.

- RandomBoundedParameterInitialisationStrategy: This is a control parameter initialisation strategy that initialises
the parameter randomly within a certain bound using some probability distribution function.

- RandomParameterInitialisationStrategy: This is a control parameter initialisation strategy that initialises the 
parameter randomly using some probability distribution function.

- SaDEIndividual: This is an individual that holds the Creation Strategy, Crossover Strategy, Parameter Adaptation
Strategies (for both, the scaling factor and the crossover probability) and the ControlParameterInitialisationStrategies
(for both, the scaling factor and the crossover probability). It holds the methods initialise( which initialises the 
individual as well as the parameters held by the creation and crossover strategies), updateParameters (which updates 
the parameters held by the creation and crossover strategies), acceptParameters (which alerts the ParameterAdaptationStrategy
for a parameter that the offspring was accepted to be in the next generation) and the getters and setters for all the variables. 

- SaDEIterationStrategy: This iteration strategy is similar to the standard DE. The difference comes in with the 
adaptation of the parameters. An SaDEIndividual needs to be used in this iteration strategy as it takes the crossover 
and creation strategies from the individual. It keeps track of when means need to be recalculated and parameters 
regenerated. 

- ConstantControlParameter: This control parameter was adapted to implement the extension of ControlParameter, 
SettableControlParameter, in order to allow for it to be set and for its update method (which performs no function) 
to be called.

# XML Examples

The algorithm used is still an EC algorithm, but i's iteration strategy changes. In order to use SADE one needs to set
the algorithm's iterationStrategy to SaDEIterationStrategy. The frequencyOfChange is how often the parameter must change
(in number of iterations), while the frequencyOfMeanRecalculation is how often the mean value should be recalculated to 
change according to the learning experience.

The individual used is an SaDEIndividual as it holds the trialVectorCreationStrategy, crossoverStrategy and their 
initialisation and adaptation strategies. The parameter which needs to change, in Qin and Suganthan's case the 
crossover probability, is set to be of type StandardUpdatableControlParameter, while the one that does not change, 
in this case the scaling factor, is set to be of type ConstantControlParameter.

The scalingFactorInitialisationStrategy and crossoverProbabilityInitialisationStrategy are set to their appropriate
ControlParameterInitialisationStrategy and the their random providers are set to have a mean of 0.5 and a standard 
deviation of 0.1 and 0.3.

XML:
    <algorithm id="de" class="ec.EC">
        <iterationStrategy class="ec.iterationstrategies.SaDEIterationStrategy" frequencyOfChange="5" frequencyOfMeanRecalculation="25"/>
        <initialisationStrategy class="algorithm.initialisation.ClonedPopulationInitialisationStrategy">
            <entityNumber value="50"/>
            <entityType class="ec.SaDEIndividual"> 
                <trialVectorCreationStrategy class="entity.operators.creation.SaDECreationStrategy">
                    <scaleControlParameter class="controlparameter.ConstantControlParameter"/>
                </trialVectorCreationStrategy>
                <crossoverStrategy class="entity.operators.crossover.de.DifferentialEvolutionBinomialCrossover">
                    <crossoverProbabilityParameter class="controlparameter.StandardUpdatableControlParameter"/>
                </crossoverStrategy>
                <scalingFactorInitialisationStrategy class="controlparameter.initialisation.RandomBoundedParameterInitialisationStrategy" lowerBound= "0" upperBound = "2">
                    <random class="math.random.GaussianDistribution" mean = "0.5" deviation = "0.3"/>
                </scalingFactorInitialisationStrategy>
                <crossoverProbabilityInitialisationStrategy class="controlparameter.initialisation.RandomParameterInitialisationStrategy">
                    <random class="math.random.GaussianDistribution" mean = "0.5" deviation = "0.1"/>
                </crossoverProbabilityInitialisationStrategy>
            </entityType>
        </initialisationStrategy>
        <addStoppingCondition class="stoppingcondition.MeasuredStoppingCondition" target="5000"/>
    </algorithm>



If there are any questions join us on [irc chat](http://webchat.freenode.net/?channels=cilib).

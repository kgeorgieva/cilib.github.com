---
layout: docs
title: "Self-Adapting Diversity Differential Evolution"
description: ""
group: "user-docs"
tags: [code, master, changes, Differential evolution, de, self-adapting]
---
{% include JB/setup %}

This describes the implementation, experiments and results of the Self-adaptive Diversity Differential Evolution 
(SaDDE) described by Efren Mezura-Montes and Gabriela Palomeque-Ortiz in their 2009 paper "Self-adaptive and 
Deterministic Parameter Control in Differential Evolution for Constrained Optimization".

# Available Algorithm Configurations
- Self Adaptive Diversity Differetial Evolution: This currently consists of a new iteration strategy that adapts 
the Diversity Differential Evolution algorithm by allowing for three parameters to be adapted in a similar manner 
to the individual and for the fourth parameter to be decreased. The first three parameters are the scaling 
factor, crossover probability and total offspring, while the decreasing parameter is the selector parameter which 
is a probability used to choose the survivor for the next generation.

# Implementation Details

- ParameterizedIndividual: This is an individual that holds the crossoverStrategy and trialVectorCreationStrategy 
of the individual. It also holds the ``total offspring'' parameter and a three dimensional individual used to 
adapt the parameters using the same strategies as for the Individual itself. 
		
- SaDDEIterationStrategy: This is the iteration strategy described in the paper. Here the offspring and new 
parameters are generated, the parameters to be kept by the offspring are chosen, an individual from all offspring 
individuals is selected, the survivor between the offspring and current individual is added to the next generation 
and the selectorParameter is modified.

# XML Examples
The XML below is designed to run the experiments as described by Mezura-Montes et al.

The offspringSelectionStrategy and nextGenerationSelectionStrategy used in the paper are both the FeasibilitySelector,
which requires a boundaryConstraint. The selectorParameterRandom is the random probability distribution to be used to
select the initial value of the scaling factor. Similarly, the lastSelectorFactorRandom is the random probability 
distribution to be used to select the initial value of the latest scaling factor value before the current one
(used to adapt the scaling factor).

The entity is set to a ParameterizedIndividual as this is the kind of individual the strategy deals with. The 
scalingFactorLowerBound and other settings in this line determine the upper and lower bounds that the 
parameters must fall within, which the parameterConstraint will enforce. The trialVectorCreationStrategy and crossoverStrategy are held by the
parameterized individual and must therefore be set here.

XML:

    <algorithm id="de" class="ec.EC">
            <iterationStrategy class="ec.iterationstrategies.SaDDEIterationStrategy">
                <offspringSelectionStrategy class="util.selection.recipes.FeasibilitySelector">
                    <constraint class="problem.boundaryconstraint.ClampingBoundaryConstraint"/>
                </offspringSelectionStrategy>
                <nextGenerationSelectionStrategy class="util.selection.recipes.FeasibilitySelector">
                    <constraint class="problem.boundaryconstraint.ClampingBoundaryConstraint"/>
                </nextGenerationSelectionStrategy>
                <selectorParameterRandom class="math.random.UniformDistribution">
                    <lowerBound class="controlparameter.ConstantControlParameter" parameter="0.45"/>
                     <upperBound class="controlparameter.ConstantControlParameter" parameter="0.65"/>
                </selectorParameterRandom>
                <lastSelectorFactorRandom class="math.random.UniformDistribution">
                    <lowerBound class="controlparameter.ConstantControlParameter" parameter="0.0"/>
                     <upperBound class="controlparameter.ConstantControlParameter" parameter="0.5"/>
                </lastSelectorFactorRandom>
            </iterationStrategy>
            <initialisationStrategy class="algorithm.initialisation.ClonedPopulationInitialisationStrategy">
                <entityNumber value="60"/>
                <entityType class="ec.ParameterizedIndividual" scalingFactorLowerBound = "0.3" scalingFactorUpperBound = "0.9" 
                    crossoverProbabilityLowerBound = "0.9" crossoverProbabilityUpperBound = "1.0" totalOffspringLowerBound = "3.0" 
                    totalOffspringUpperBound = "7.0" >
                    <initializationStrategy class="entity.initialization.RandomBoundedInitializationStrategy">
                        <lowerBound class="controlparameter.ConstantControlParameter" parameter="-5.12"/>
                        <upperBound class="controlparameter.ConstantControlParameter" parameter="5.12"/>
                    </initializationStrategy>
                    <trialVectorCreationStrategy class="entity.operators.creation.RandCreationStrategy"/>
                    <crossoverStrategy class="entity.operators.crossover.de.DifferentialEvolutionBinomialCrossover"/>
                    <parameterConstraint class="problem.boundaryconstraint.ClampingBoundaryConstraint"/>
                    
                </entityType>
            </initialisationStrategy>
            <addStoppingCondition class="stoppingcondition.MeasuredStoppingCondition" target="600"/>
     </algorithm>


If there are any questions join us on [irc chat](http://webchat.freenode.net/?channels=cilib).

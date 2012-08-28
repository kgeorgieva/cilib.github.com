---
layout: docs
title: "Self-Adapting Differential Evolution"
description: ""
group: "user-docs"
tags: [code, master, changes, Differential evolution, de, self-adapting]
---
{% include JB/setup %}

This describes a number of self-adaptive Differential Evolution strategies that have been implemented.
The first is the self-adapting DE described by A. K. Qin and P. N. Suganthan in their 2005 IEEE
paper "Self-adaptive Differential Evolution Algorithm for Numerical Optimization". 



# Available Algorithm Configurations
- Self Adaptive Differetial Evolution: This currently consists of a new probability based trial vector 
creation strategy.

# Implementation Details

## Qin and Suganthan's Self Adaptive DE
-SaDECreationStrategy: This is a trial vector creation strategy which uses an adapting probability to 
choose one of two creation strategies that will be used to generate a trial vector for a particular 
individual. At first there is an equal probability to choose both strategies. As time passes, the 
probability is adapted depending on the total number of offspring surviving to the next generation, 
making the more successful creation strategy more likely to be chosen.


# XML Examples

## Qin and Suganthan's Self Adaptive DE
To use the Self-adaptive Trial Vector creation strategy described by Qin and Suganthan the
iterationStrategy must be given SaDECreationStrategy as the class of the trialVectorCreationStrategy.

XML:
    <algorithm id="de" class="ec.EC">
        <iterationStrategy class="ec.iterationstrategies.DifferentialEvolutionIterationStrategy">
            <trialVectorCreationStrategy class="entity.operators.creation.SaDECreationStrategy"/>
        </iterationStrategy> 
    </algorithm>



If there are any questions join us on [irc chat](http://webchat.freenode.net/?channels=cilib).

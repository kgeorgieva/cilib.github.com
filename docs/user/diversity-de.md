---
layout: docs
title: "Diversity Differential Evolution"
description: ""
group: "user-docs"
tags: [code, master, changes, Differential evolution, de, self-adapting]
---
{% include JB/setup %}

This describes the Diversity Differential Evolution algorithm described by Efren Mezura-Montes and 
Gabriela Palomeque-Ortiz in their 2009 paper ["Self-adaptive and Deterministic Parameter Control 
in Differential Evolution for Constrained Optimization"](http://www.lania.mx/~emezura/util/files/mezura-palomeque-chapter.pdf).
 Their algorithm adapts the standard Differential Evolution algorithm through a number of additions:

- Allowing the target vector to generate more than one offspring and choosing the best offspring 
from the resulting set.
- A new selection method that chooses:
    * The vector with the best fitness value if all vectors are feasible.
    * The feasible vector if there is a feasible and infeasible one.
    * The vector with the lowest sum of constraint violation if all are infeasible.
- A new selection parameter which determines how the selection process will take place, using purely 
fitness or taking into account feasibility as well.

## Available Algorithm Configurations
- Diversity Differetial Evolution: The original Implementation of the Diversity Differential Evolution algorithm
has been implemented, as described in  Mezura-Montes et al's paper.

## Implementation Details

- FeasibilitySelector: this is a selector that chooses between feasible and infeasible solutions according 
to the above mentioned rules. It has been developed to allow for selection for more than just two vectors.

- DDEIterationStrategy: This is the iteration strategy that allows the trial vector to choose the best 
offspring of $No$ offspring (where $No$ is the total number of offspring to select from). It also adds a 
check for the selection process that should be used to select the survivor for the next generation 
(a feasibility based one or a fitness based one).

- UniformDistribution: This class was adapted to include getters and setters for the already existing lower and upper bound parameters.

## XML Examples

Below is an example of the XML required to run a DDE algorithm. Here:

- The selectorParameter refers to the value of the parameter used to choose between the selection strategies to be used
- The totalOffspring refers to the total number of offspring that must be generated from a target vector in order to choose 
the best from as set
- The offspringSelectionStrategy refers to the selector to be used in order to determine which offspring is better
- The nextGenerationSelectionStrategy refers to the selector to be used in order to select which individual survives to the 
next generation
- The constraint refers to the constraint used on the individuals
- As the constraint is a Boundary constraint, the bounds are given in the initialisationStrategy as the lower and upper
bounds.

        <algorithm id="dDe" class="ec.EC">
            <iterationStrategy class="ec.iterationstrategies.DDEIterationStrategy" selectorParameter="0.45" totalOffspring="2">
                <offspringSelectionStrategy class="util.selection.recipes.FeasibilitySelector">
                    <constraint class="problem.boundaryconstraint.ClampingBoundaryConstraint"/>
                </offspringSelectionStrategy>
                <nextGenerationSelectionStrategy class="util.selection.recipes.FeasibilitySelector">
                    <constraint class="problem.boundaryconstraint.ClampingBoundaryConstraint"/>
                </nextGenerationSelectionStrategy>
            </iterationStrategy>
            <initialisationStrategy class="algorithm.initialisation.ClonedPopulationInitialisationStrategy">
                <entityNumber value="50"/>
                <entityType class="ec.Individual">
                    <initializationStrategy class="entity.initialization.RandomBoundedInitializationStrategy">
                        <lowerBound class="controlparameter.ConstantControlParameter" parameter="-5.12"/>
                        <upperBound class="controlparameter.ConstantControlParameter" parameter="5.12"/>
                    </initializationStrategy>
                </entityType>
            </initialisationStrategy>
            <addStoppingCondition class="stoppingcondition.MeasuredStoppingCondition" target="5000"/>
        </algorithm>


If there are any questions join us on [irc chat](http://webchat.freenode.net/?channels=cilib).

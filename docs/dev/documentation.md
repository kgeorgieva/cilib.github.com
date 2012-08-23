---
layout: docs
title: "Creating User Documentation Pages"
group: "dev-docs"
description: ""
---
{% include JB/setup %}

This document describes what documentation is expected from developers when new code is contributed to Cilib. It is assumed that you have already followed the instructions to [get started on the Cilib website](website-configuration.html).

## User Documentation Pages
User documentation pages are intended for both developers and non-developers who want to use the library to create and execute computational intelligence (CI) algorithms. The pages must be easy to read and understand (although basic knowledge of CI systems can be assumed) and should not contain excessive or unnecessary programming details.

### User Documentation Layout and Structure
A user documentation page should focus on a single algorithm or CI technique that is available in Cilib. For example, a page describing the use of the standard PSO implementation. The following sections are recommended:

* #### Introduction
The introduction should be the first body of text on the page, giving a short overview of the implementation. Citation to the original and other relevant publications may be useful in this section. The introduction should not have a section heading.

* #### Available Algorithm Configurations
This section should describe the possible configurations that can be achieved with Cilib. For example, this section of the standard PSO documentation should include the use of synchronous and asynchronous iteration strategies.

* #### Implementation Details
In this section, a short description of the relevant classes should be given. Avoid overly complicated explanations. Simply state the name and purpose of each class.

* #### [Optional] Additional Sections
If you require further sections to clarify the use of your code, additional sections may be added here.

* #### XML Examples
Finally, provide at least one XML example to show how to construct a configuration using the implementation described in your documentation.

## Creating Your Documentation Pages

### Step 1: Create a new file
For each user documentation page, a `*.md` file should be created in the `docs/user` folder. Please name the file appropriately and use `-` instead of spaces. Place the following header in the file:

	---
	layout: docs
	title: "Your Title"
	group: "user-docs"
	description: ""
	---
	{ % include JB/setup % }

### Step 2: Create your sections and write up the documentation
The following code is a skeleton template for documentation pages. Place this code in your `*.md` file under the header.

	This is my introduction

	# Available Algorithm Configurations

	- Configuration 1: This is a description of the first configuration.
		
	- Configuration 2: This is a description of the second configuration.

	# Implementation Details

	## Configuration 1
	- Class 1: This describes the purpose of class 1 in configuration 1.
		
	- Class 2: This describes the purpose of class 2 in configuration 1.

	## Configuration 2
	- Class 1: This describes the purpose of class 1 in configuration 2.
		
	- Class 2: This describes the purpose of class 2 in configuration 2.

	# XML Examples

	## Configuration 1

	This is an explanation of any parts of the xml for configuration 1 that may require clarification.

	XML:

			<this is>
			    <an xml>
				<example/>
			    </an xml>
			</this is>

For more examples, take a look at the documentation pages already in `docs/user`.

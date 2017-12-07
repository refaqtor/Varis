<p align="center">
    <img src="examples/gopher.jpg" height="200" alt="Gopher from internet =)" title="Gopher from internet =" />
</p>

# Varis
Neural Networks with GO

[![Build Status](https://travis-ci.org/Xamber/Varis.svg?branch=master)](https://travis-ci.org/Xamber/Varis)
[![Go Report Card](https://goreportcard.com/badge/github.com/Xamber/Varis)](https://goreportcard.com/report/github.com/Xamber/Varis)
[![API Reference](https://camo.githubusercontent.com/915b7be44ada53c290eb157634330494ebe3e30a/68747470733a2f2f676f646f632e6f72672f6769746875622e636f6d2f676f6c616e672f6764646f3f7374617475732e737667)](https://godoc.org/github.com/Xamber/Varis)
[![codecov](https://codecov.io/gh/Xamber/Varis/branch/master/graph/badge.svg)](https://codecov.io/gh/Xamber/Varis)
[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/xamber/Varis/blob/master/LICENSE.md)

## Disclaimer
Some time ago I decided to learn Go language and neural networks.
And the best way is to do it - practice. So I use this repository to better understand the language.
I've already encountered many pitfalls in GO, I've learned in practice many tools, data types and "chips" of the language.
I would be happy if someone can find errors and give advice.

Thank you. Artem.

## About package
- No dependencies
- All neurons and synapses are goroutines.
- Golang channels for connecting neurons.
- Neuron have callback function for redirect signal to output or any place you want.

## Installation
    go get https://github.com/Xamber/Varis

## Usage
```go
package main

import (
	"github.com/xamber/Varis"
)

func main() {
	n := varis.CreatePerceptron(2, 3, 1)

	dataset := varis.Dataset{
		{varis.Vector{0.0, 0.0}, varis.Vector{1.0}},
		{varis.Vector{1.0, 0.0}, varis.Vector{0.0}},
		{varis.Vector{0.0, 1.0}, varis.Vector{0.0}},
		{varis.Vector{1.0, 1.0}, varis.Vector{1.0}},
	}

	varis.BackPropagation(&n, dataset, 10000)
	varis.PrintCalculation = true

	n.Calculate(varis.Vector{0.0, 0.0})
	n.Calculate(varis.Vector{1.0, 0.0})
	n.Calculate(varis.Vector{0.0, 1.0})
	n.Calculate(varis.Vector{1.0, 1.0})

	// Model example section
	type Model struct {
		Network *varis.Perceptron
		X1      varis.BooleanField `direction:"input"`
		X2      varis.BooleanField `direction:"input"`
		O       varis.BooleanField `direction:"output"`
	}

	f := Model{Network: &n}

	calculate := varis.GenerateRunFunction(f)

	calculate([]interface{}{false, false})
	calculate([]interface{}{true, false})
	calculate([]interface{}{false, true})
	calculate([]interface{}{true, true})
}

```
## Roadmap
- Improve project structure.
- Add error return to functions.
- Create more tests and benchmarks.
- Create normal documentation.
- Implement Models (Normalize data from bool, integer, array etc.)
- Create signal and weight types.



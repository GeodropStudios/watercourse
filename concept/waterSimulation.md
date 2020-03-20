# Water Simulation

This document presents ideas on how water simulation could be implemented in the game. The goal is a light-weight interactive system that is able to simulate and render the flow of a single stream of water down a terrain mesh.


### Proposal 1: Metaballs

Simulating liquid through [metaballs](https://en.wikipedia.org/wiki/Metaballs) has been done before, and could be an option for making the river. Creating lots of metaballs and letting them represent a liquid, letting them run down the terrain surface, would create the river. It might be heavy on computation, but would likely give a realistic behavior that is relatively easy to implement. Making river forks and lakes would be done automatically this way.

### Proposal 2: Directed Acyclic Graph (DAG) for flow network

Constructing a DAG representing the river's flow, where each node is associated with a point on the surface that is the terrain. Constructing the DAG could be done through iteratively using the gradient of the terrain surface, defining a line along which the river runs. This would not be very heavy on computation, but rendering a realistic river following the curve would be challenging. Lakes would probably be possible in some way, and river forks are allowed in a DAG, the problem is just how to determine where forks and lakes should occur.

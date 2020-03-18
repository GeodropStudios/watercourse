# Gradient graph construction algorithm

## Gradient graph

A directed acyclic graph (DAG) where each node holds a set of 3D coordinates that are on the terrain surface. Geometric direction is inferred, available through the difference of the points of two subsequent nodes.

The point is to have a start node, with coordinates that lie within some triangle. Following the negative gradient of the triangle, the next node is on the nearest intersection point between the negative gradient direction and a grid line. Continue with the triangle adjacent to the encountered grid line. The last point is on the first grid line reached where there is no adjacent triangle.

## Construction algorithm

Input: Terrain surface (unstructured triangle grid) T, start point P.

Output: DAG R

Procedure:

```
makeRiver(T, P) {
  DAG R;
  R.append(node(P));
  d = gradient(T.triangleAtPoint(P));
  P' = firstIntersection(ray(P, d), T);
  R.append(node(P'));
  while (T.adjacentTriangleCount(T.lineAtPoint(P')) > 1) {
    d = gradient(T.nextTriangle(P', d));
    P' = firstIntersection(ray(P', d), T);
    R.append(node(P'));
  }
  return R;
}
```

## Problems to be solved

- How should the helper functions in the algorithm be implemented?
- What happens when the gradient points toward a triangle vertex? Which is the next triangle?
- How is a smooth and still realistic curve produced from the graph? How is the curve rendered?
- Should 2D coordinates be stored, and in rendering should the points be projected onto the surface?

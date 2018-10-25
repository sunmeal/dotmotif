<p align="center">
  <img align="center" src="./logo.png" / width="25%">
  <h1 align="center" fontsize="2em">d o t m o t i f</h1>
</p>
<p align="center">find brain-graph motifs using friendly notation</p>

# Usage

## Writing a motif

You can currently write motifs in dotmotif form, which is a DSL that specializes in subgraph query notation.

`threecycle.motif`
```
# A excites B
A -+ B
# B inhibits C
B -| C
```

## Ingesting the motif into dotmotif

```python
from dotmotif import dotmotif

dm = dotmotif().from_csv("threecycle.csv")

# or:
dm = dotmotif().from_motif("threecycle.motif")
```

You can also pass optional parameters into the constructor for the `dotmotif` object. Those arguments are:

| Argument | Type, Default | Behavior |
|----------|------|----------|
`ignore_direction` | `bool`: `False` | Whether to disregard direction when generating the database query |
| `limit` | `int`: `None` | A limit (if any) to impose on the query results |
| `enforce_inequality` | `bool`: `False` | Whether to enforce inequality; in other words, whether two nodes should be permitted to be aliases for the same node. For example, A>B>C; if A!=C, then set to True |

## Generating the Query

This will return a string query:

```python
dm.to_cypher() # "MATCH (A:Neuron)-[:SYN]-> ..."
```

You can chain the entire operation into one single command using the chaining functionality of this library:

```python
dm = dotmotif().from_motif("threecycle.motif").to_cypher()
```

For more details on how to write a query, see [Getting Started](docs/start.md).

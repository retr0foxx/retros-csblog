---
layout: post
title: "Scrapped: Basics of Max Flow"
date: 2100-05-01
math: katex
---

This blog post, which is basically the first blog post in this site, will teach you about *max flow!*

First and foremost, we will give the formal definition of the problem of a flow network.

A flow network is a *directed* graph $(V, E)$ with two special vertices $s, t \in V$ ($s \neq t$) such that each edge $e \in E$ has a *capacity* $c(e)$ and a flow $f(e)$ where $0 \leq f(e) \leq c(e)$ which satisfy the property that for all $v \in V \backslash \{s, t\}$, it follows that $\sum_{u, (u, v) \in E}f((v, u)) = \sum_{u,(u, v) \in E} f((u, v))$. Moreover, $\sum_{u,(u, s) \in E} f((u, s)) = 0$ and $\sum_{u,(t, u) \in E} f((t, u)) = 0$.

Note on notation: The parts such as "$u, (u, v) \in E$" in the sums above simply means "all u, such that (u, v) is an edge within the graph"

Of course, this formal definition does not help anyone understand what exactly the problem is. So, an explanation of the problem in more clear English will be given. We have a directed graph, with two special vertices $s$ and $t$, called the *sink* and the *source*. We imagine the source as a vertex which is able to give an arbitrary amount of "flow" and the sink as a vertex which is able to receive an arbitrary amount of "flow." Each edge in the graph has a capacity $c(e)$ denoting the maximum amount of *flow* that can pass through it. Each edge also has an ongoing flow $f(e)$. Of course, it must be the case that the flow going through an edge must not exceed the capacity of the edge. Also, it must be the case that for each vertex *other than the source and the sink*, the amount of flow going into it must be equal to the amount of flow going out of it. Finally, there can only be flow going *out* of the source, with none going in, and conversely, there can only be flow going into the sink, with none going out.

So, the key holding a flow network are simply the following parts of its definition:
- The source only has flow going out of it, and conversely, the sink only has flow going into it.
- The amount of flow going into a vertex must be equal to the amont of flow going out of the vertex.

Those are the key parts of the definition that is holding the structure of the flow network. Now, given those definitions, we can finally infer some basic information about a flow network.

The first one of those is that **the amount of flow leaving the source equals the amount of flow entering the sink.** Before reading the rest, try proving it yourself first. 

The idea is simple, we imagine that we initially have the set $S = \{s\}$, and we slowly add into the set, vertices currently directly adjacent to the set (i.e. vertices $v$ where there exists an element of the set $u$ where $(u, v) \in E$), and see that whenever any directly reachable vertex is added, the following property of the set is always mantained: the total amount of flow leaving the set, substracted by the total amount entering the set, equals the flow given out by $s$. If there is a way to do this such that eventually $S$ satisfy that every edge $(u, t)$ with non-zero flow has $u \in S$, then we would have finished the proof, since it means the total flow going into $t$ equals the total flow properly leaving $S$ without re-entering. So, let's get to proving.

- Let $C$ denote the total amount fo flow leaving $s$. More formally, $C = \sum_{(s, u) \in E} f((s, u))$.
- For a set $S$, let $F(S)$ denote the flow leaving $S$ and $G(S)$ denote the flow entering $S$.
- Formally given a set $S$, $F(S) = \sum_{u \in S, v \notin S, (u, v) \in E} f((u, v))$ while $G(S) = \sum_{u \notin S, v \in S, (v, u) \in E}$.
- Initially, define $S = \{s\}$.
- Initially, $F(S) - G(S) = C$ is true by definition of $s$, which is that no flow enters $s$, hence $G(S) = 0$ while $F(S) = C$.
- We shall prove that adding any vertex $v \notin S$ with $v \neq t$ such that there exists a $u \in S$ where $(u, v) \in E$ mantains the property that $F(S) - G(S) = C$.
...
- Thus, as long as there still exists a $v \notin S$ and $v \neq t$ such that there exists a $u \in S$ where $(u, v) \in E$, we can keep adding it into the set.
- Now, it must be the case that $F(S) = C$. 
---
title       : "Graphs"
excerpt     : "Graphs"
sitemap     : false
permalink   : /docs/mit_6_006_06/
toc         : true
---

<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/0VqSdtXseb9khdZrnYVyM1?utm_source=generator" width="100%" height="152" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>

## Graphs
![full](https://hostux.social/system/media_attachments/files/109/804/548/602/575/430/original/cbb65011365039fe.jpeg){: .full}
### Graph Search
Explore a graph, e.g:
* find a path from start vertex s to a desired vertex
* visit all vertices or edge of graph, or only those reachable from s
### Graph Representations
![full](https://hostux.social/system/media_attachments/files/109/804/613/153/132/186/original/1a6d45ebe4b4a058.jpeg){: .full}
### Breadth First Search
* level 0={s}
* level = vertices reachable by path of i edges but not fewer
* build level i>0 from level i-1 by trying all outgoing edges, but ignoring vertices from previous levels
* O(V+E) (Linear time)
![full](https://hostux.social/system/media_attachments/files/109/804/652/056/330/475/original/c534c36984630b71.jpeg){: .full}
#### Shortest Paths
![full](https://hostux.social/system/media_attachments/files/109/804/683/422/058/590/original/433d9cc452403234.jpeg){: .full}
### Depth First Search
![full](https://hostux.social/system/media_attachments/files/109/804/708/295/934/406/original/a5bafc7f389b36bc.jpeg){: .full}
![full](https://hostux.social/system/media_attachments/files/109/804/716/143/867/728/original/9cc8476cfb435029.jpeg){: .full}
![full](https://hostux.social/system/media_attachments/files/109/804/724/896/674/853/original/51b5089bee94bc90.jpeg){: .full}
### Cycle Detection
Graph G has a cycle <=> DFS has a back edge
![full](https://hostux.social/system/media_attachments/files/109/804/738/728/755/547/original/e28fe1ffba604ecf.jpeg){: .full}

## Source
[https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/pages/lecture-notes/](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/pages/lecture-notes/)

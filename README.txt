SMALE HANDLE DECOMPOSITION VIEWER FOR SURFACES (VIA ROTATION SYSTEMS)
======================================================================

Version 1.0.0
File: index.html (single self-contained HTML file)
Interface language: Ukrainian / English (toolbar toggle)

An interactive browser-based program that visualizes Smale handle
decompositions for closed oriented and non-orientable surfaces based on a
rotation system code. The tool builds a geometric unfolding, glues it into
handles (0-handles as disks/circles, 1-handles as ribbons, 2-handles as
capping disks), displays the Morse flow (and reversed flow) on the surface,
draws the Fomenko atom (critical level set and its neighborhood), and
performs elementary handle operations (1-handle slide, 0-1 and 1-2
cancellations, 0-1 and 1-2 births).

The program is a single self-contained HTML file: no installation, no server,
no external dependencies; it works offline in any modern web browser (Chrome,
Edge, Firefox, Safari). Simply open index.html to begin.

Run online:  https://<LOGIN>.github.io/<REPOSITORY>/
(replace <LOGIN> and <REPOSITORY> with your GitHub user name and repository
name)

  Author:    Alexandr Prishlyak (Taras Shevchenko National University of
             Kyiv), ORCID 0000-0002-7164-807X
  License:   MIT (see the file LICENSE)
  DOI of this version: 10.5281/zenodo.23879705
  Related software:
    - Rotation-system codes: enumeration and visualization of cellular
      graph embeddings. DOI 10.5281/zenodo.23404153
      https://doi.org/10.5281/zenodo.23404153
    - Flows and bifurcations: MS, SN, SC.
      DOI 10.5281/zenodo.23764761
      https://doi.org/10.5281/zenodo.23764761


----------------------------------------------------------------------
1. INPUT: ROTATION SYSTEM CODE (ORIENTED AND NON-ORIENTABLE SURFACES)
----------------------------------------------------------------------

Example (loaded on startup):  1 3 2 0 1 5 0 2 3 4 5 4 00 +-+-+

* Numbers specify the names of half-handles; each handle number must appear
  exactly twice (once for each end). A number appearing only once is drawn
  without a curve.
* 0 separates words. Each word corresponds to a Smale 0-handle (initially
  drawn as a polygon that transforms into a circle): the numbers in the word
  are the 1-handles (ribbons) attached to it in counter-clockwise order.
  The example contains three 0-handles: "1 3 2", "1 5", and "2 3 4 5 4".
* After 00, an optional list of signs (twists) defines the orientability of
  the surface:
    +  untwisted 1-handle (oriented attachment);
    -  1-handle with a half-twist (non-orientable / twisted attachment).
  The i-th sign corresponds to the i-th handle in ascending numerical order.
  The list +-+-+ twists handles 2 and 4 (yielding a non-orientable surface).
  If 00 is omitted, all handles default to + (producing an oriented
  surface).
* The first occurrence of a number is labeled A, and the second is labeled B
  (3A, 3B, ...).


----------------------------------------------------------------------
2. UNFOLDING OF 0-HANDLES AND 1-HANDLE CURVES
----------------------------------------------------------------------

* A word with k numbers is rendered as a regular polygon with 2k + e sides
  (e is the "Extra sides" field, default 4, minimum 0; at least 3 sides).
* Numbers are assigned to every second side counter-clockwise; unassigned
  sides face areas with fewer neighboring polygons.
* 0-handles (polygons) are distributed along a circle. The distance between
  centers is at least two diameters of the largest 0-handle (adjustable via
  the Distance slider).
* Sides sharing the same number are joined by Bezier curves representing the
  axes of 1-handles. A draggable node (white circle) is placed at the
  midpoint of each curve.
* Arrange recalculates the placement of 0-handles, their rotations, and text
  alignments by minimizing a penalty function (curve intersections, overlap
  with foreign 0-handles, etc.).
* Loops (both ends of a 1-handle on the same 0-handle): the control node is
  positioned along the perpendicular bisector at a distance between 1.5 R
  and 3.5 R from the disk.
* SVG exports the current unfolding and handle layout to a vector SVG file.


----------------------------------------------------------------------
3. GLUING SMALE 1-HANDLES
----------------------------------------------------------------------

* Under the Glue toolbar, select the numbers (checkboxes) of the 1-handles
  to be glued.
* The play / pause button and progress slider animate the gluing process:
  the centers of the two ends of a 1-handle travel along the Bezier curve
  toward its midpoint to form a 1-handle (ribbon). The center of the glued
  boundary segment corresponds to a saddle point (index-1 critical point).
* Twists (non-orientable case): a 1-handle marked with "-" features a
  half-twist (modeling non-orientable embedding). It is rendered with two
  crossing boundary lines, where one line is interrupted to visually
  indicate an underpass.


----------------------------------------------------------------------
4. MORSE FLOW ON THE DECOMPOSITION
----------------------------------------------------------------------

The Morse flow button cycles through three states:
flow -> reversed flow -> hidden.

* The center of each 0-handle (disk) contains a source / Morse function
  minimum (index 0) (red dot).
* Red separatrices originate from the source, pass through the centers of
  glued edges along the 1-handle, and terminate at the saddle / index-1
  critical point (black dot).
* Glued edges are replaced by two green directed line segments pointing from
  the saddle toward the boundary.
* Blue regular trajectories leave the sources and flow toward the surface
  boundary and alongside separatrices.
* Smale 2-handles (maxima / index 2): the complement of 0- and 1-handles
  (boundary components) is capped by 2-handles, which act as sinks for the
  flow.
* Reversed flow: red and green elements swap roles (sources become sinks),
  and all trajectory direction arrows are reversed.


----------------------------------------------------------------------
5. SMALE HANDLE DECOMPOSITION VIEW
----------------------------------------------------------------------

The Handle decomposition button displays the standard topological handle
layout:

* 0-handles: solid disks with a central black dot (minimum) and blue word
  label;
* 1-handles: ribbons attached to the 0-handle disks;
* Separatrices: red and green separatrices are rendered as dashed lines
  outside the 0-handles.


----------------------------------------------------------------------
6. FOMENKO ATOM
----------------------------------------------------------------------

The Atom button visualizes the Fomenko atom (the critical level set of the
Morse function together with its neighborhood):

* A central hole (puncture) is carved out of each 0-handle disk;
* Solid black curves represent the critical level set: four rays emanate
  from each saddle at 45 degrees relative to the glued edge, travel along the
  1-handles, and form the graph structure of the atom.
* For twisted (non-orientable) 1-handles, the critical level curves split to
  reflect the half-twisted topology.


----------------------------------------------------------------------
7. HANDLE MODIFICATIONS AND OPERATIONS
----------------------------------------------------------------------

Select an operation from the Operation menu and a target half-handle (3A,
3B, ...), then use the play button (animation) and the check mark (apply:
updates the rotation system code):

1. 1-Handle Slide. Direction "<- L" or "R ->". The foot of the selected
   1-handle slides along an adjacent 1-handle to its opposite side. If the
   adjacent 1-handle is non-orientable (marked "-"), the sign of the sliding
   handle flips.
2. 0-1 Cancellation (minimum-saddle elimination). Applicable when a 0-handle
   contains only one end of the 1-handle (a word of length 1). The 0-handle
   and 1-handle cancel out.
3. 1-2 Cancellation (saddle-maximum elimination). A 1-handle is removed if
   its lateral edges belong to distinct boundary components (different
   2-handles).
4. 0-1 Birth (minimum-saddle creation). Spawns a new 0-handle disk along
   with a connecting 1-handle.
5. 1-2 Birth (saddle-maximum creation). Splits a boundary component to
   insert a new 1-handle pair.


----------------------------------------------------------------------
8. EXAMPLES
----------------------------------------------------------------------

Code                                | Description                  | Surface
------------------------------------+------------------------------+--------------
1 3 2 0 1 5 0 2 3 4 5 4 00 +-+-+    | 3 0-handles, twisted         | Non-orientable
                                    | 1-handles 2 and 4            |
1 3 2 0 1 0 2 3                     | Basic example, 3 0-handles   | Oriented
                                    | and oriented 1-handles       |
1 3 2 3 4 1 2 4                     | Single 0-handle, all         | Oriented
                                    | 1-handles are loops          |
1 3 2 5 3 1 2 4 5 4                 | Nested loops on a single     | Oriented
                                    | 0-handle                     |
1 2 3 0 1 0 2 3                     | Ready for 0-1 cancellation   | Oriented
                                    | of handle 1                  |
1 2 0 1 2                           | 1-2 cancellation possible    | Oriented
                                    | for both handles             |


----------------------------------------------------------------------
9. KNOWN LIMITATIONS
----------------------------------------------------------------------

* 0-1 cancellation for non-orientable (twisted) handles executes geometric
  adjustments in a simplified mode (updates code and signs).
* 1-2 cancellation and both birth operations are experimental features
  (exact combinatorial code transformations with simplified animations).
* The Arrange button uses a time-bounded heuristic (0.3 s during typing, 2 s
  on manual click). Curve nodes can be manually dragged if minor overlaps
  persist.


----------------------------------------------------------------------
10. CITATION
----------------------------------------------------------------------

A. Prishlyak. Smale Handle Decomposition Viewer for Surfaces (via Rotation
Systems), Version 1.0.0. Zenodo, 2026. DOI: 10.5281/zenodo.23879705.
https://doi.org/10.5281/zenodo.23879705


----------------------------------------------------------------------
11. REFERENCES
----------------------------------------------------------------------

1. A. Prishlyak. Codes of Rotation Systems of a Cell-Embedded Graph in an
   Oriented Surface [Computer software]. Zenodo, 22298943, 2026.
   https://doi.org/10.5281/zenodo.22298943
2. A. Prishlyak. One-Cycle Signed Chord Diagrams [Computer software].
   Zenodo, 23084341, 2026. https://doi.org/10.5281/zenodo.23084341
3. Prishlyak, A. (2026). Rotation-system codes: enumeration and
   visualization of cellular graph embeddings (Version 1.0.0) [Computer
   software]. Zenodo. https://doi.org/10.5281/zenodo.23404153
4. J. L. Gross, T. W. Tucker. Topological Graph Theory. Wiley, New York,
   1987 (Dover reprint, 2001).
5. B. Mohar, C. Thomassen. Graphs on Surfaces. Johns Hopkins University
   Press, Baltimore, 2001.
6. S. K. Lando, A. K. Zvonkin. Graphs on Surfaces and Their Applications.
   Encyclopaedia of Mathematical Sciences 141, Springer, 2004.
7. A. O. Prishlyak. On graphs embedded in a surface. Russ. Math. Surv.,
   52(4):844-845, 1997. DOI: 10.1070/RM1997v052n04ABEH002074
8. J. Edmonds. A combinatorial representation for polyhedral surfaces.
   Notices Amer. Math. Soc. 7 (1960), 646.
9. W. S. Massey. A Basic Course in Algebraic Topology. Graduate Texts in
   Mathematics 127, Springer, 1991.
10. G. K. Francis, J. R. Weeks. Conway's ZIP proof. Amer. Math. Monthly 106
    (1999), 393-399.
11. F. Takens. Forced oscillations and bifurcations. Comm. Math. Inst.
    Rijksuniversiteit Utrecht 3 (1974), 1-59.
12. A. Prishlyak, I. Ovtsynov. Optimal codimension one gradient flows on
    closed surfaces. Proceedings of the International Geometry Center,
    18(1): 69-101, 2025. DOI: 10.15673/pigc.v18i1.2835
13. Yu. A. Kuznetsov. Elements of Applied Bifurcation Theory, 3rd ed.
    Applied Mathematical Sciences 112, Springer, 2004.
14. M. M. Peixoto. On the classification of flows on 2-manifolds. In:
    Dynamical Systems (Proc. Sympos., Univ. Bahia, Salvador, 1971),
    Academic Press, 1973, 389-419.
15. Z. Kybalko, A. Prishlyak, R. Shchurko. Trajectory equivalence of optimal
    Morse flows on closed surfaces. Proc. Int. Geom. Cent., 11(1):12-26,
    2018. DOI: 10.15673/tmgc.v11i1.916
16. A. Prishlyak, I. Ovtsynov. The structure of Morse flows and co-dimension
    one gradient flows on the sphere with holes. Memoirs on Differential
    Equations and Mathematical Physics, 97: 137-158, 2026.
17. B. I. Hladysh, A. O. Prishlyak. Deformations in the general position of
    the optimal functions on oriented surfaces with boundary. Ukrainian
    Mathematical Journal, 71(8): 1173-1185, 2020.
18. A. V. Bolsinov, A. T. Fomenko. Integrable Hamiltonian Systems: Geometry,
    Topology, Classification. Chapman & Hall/CRC, 2004.
19. A. O. Prishlyak. Topological equivalence of smooth functions with
    isolated critical points on a closed surface. Topology Appl. 119
    (2002), 257-267.

===============================================================
Digital Geometry: Digital Model and Elementary Digital Topology
===============================================================
:author: David Coeurjolly




Digital Model
=============


Principles
----------

**Idea**

*Take benefit from the regular structure of the lattice to enhance geometrical analysis of shapes*

* Integer based computations
* Combinatorial algorithms
* high performance algorithms
* ...

.. list-table::

  * - .. image:: _static/images/sci1.*
       :width: 60%
       :align: center
    - .. image:: _static/images/sci2.*
       :width: 60%
       :align: center
    - .. image:: _static/images/sci3.*
       :width: 60%
       :align: center


Approach
--------


   .. image:: _static/images/discretnb.*
      :width: 50%
      :align: center


What do we need ?
-----------------

* *Grid/Lattice* to define our cells
* *Digital Topology* to add, at least, a combinatorial structure on cells
* *Digitization schemes* to fill the gap between Euclidean/Digital worlds
* *Fundamental objects* (straight lines, circles, planes, ...)
* *Axioms*
* **Specific Algorithms**


Lattice and Tilings
-------------------

**Requirements**

* Simplicity of the structure (storage, ...)
* Pixels access (coordinate system)
* Neighbors pixel access
* Consistency w.r.t. acquisition devices or processing pipeline
* Capacity (Information theory)

**More formally**

* *Packing Density*:  fraction of the volume filled by a given collection of solids. Given a large  number of equal Euclidean balls centered in the grid points, this quantity say how efficiently they are packed
* *Kissing Number*:  the number of neighboring balls that each ball touch
* *Covering*:  the least dense way to cover the space with equal overlapping balls



Example in dimension 2
----------------------


   .. image:: _static/images/pavages_bizarres.*
      :width: 60%
      :align: center



Definitions
-----------

**Lattice**

Given a basis `(v_1,\ldots,v_n)`:math: of `\mathbb{R}^n`:math:,


   .. math::
      \Lambda= \left \{ \sum_{i=1}^n a_iv_i \,|\, a_i \in \mathbb{Z} \right \}


(finitely-generated free abelian group, symmetry group, ...)


**Five fundamental lattices in the Euclidean plane**


  .. image:: _static/images/1000px-2d-bravais.*
      :width: 60%
      :align: center


Paving
------

**Definition** (dual lattice structure)
 The cell of a lattice point `\lambda\in\Lambda`:math: is its *Voronoi* cell



* Following fundamental lattice classification: pavings by squares, hexagons, triangles, rhombi and parallelograms.

* By definition, the paving induced by a lattice is periodic

* Triangular/Hexagonal lattice/paving are dual



  .. image:: _static/images/pavage_maillage.*
      :width: 70%
      :align: center



*Speaking of density packing/kissing number and covering, hexagonal lattice is optimal*

Dimension 3
-----------

**Regular cubic grid**

    .. math::
         V=\left ( \begin{array}{ccc}
         1 &0 &0\\
         0 & 1 &0\\
         0 & 0 & 1
         \end{array} \right )


**Face-centered cubic grid**

  .. math::
         V_{fcc}=\left ( \begin{array}{ccc}
         1 &1 &0\\
         1 & 0 &1\\
         0 & 1 & 1
         \end{array} \right )



**Body-centered cubic grid**

   .. math::
         V_{bcc}=\left ( \begin{array}{ccc}
         1 &1 & -1\\
         1 & -1 &1\\
         -1 & 1 & 1
         \end{array} \right )




  .. image:: _static/images/fccbcc.*
      :width: 45%
      :align: center

Dimension 3 (bis)
-----------------


  .. image:: _static/images/fccbcc.*
      :width: 60%
      :align: center



* **BCC** has optimal covering
* **FCC** has highest packing density and largest kissing number
* **FCC** and **BCC** are dual

   .. math::
      V_{fcc}^{-1} = V_{bcc}^T


**Hexagonal grid**

    .. math::
       V_{hexa}=\left ( \begin{array}{ccc}
         \sqrt{3}/2 & 0 \\
         1/2 &1
         \end{array} \right )

Semi-regular pavings
--------------------

**Definition**

* Several convex tiles paving the plane
* No T-junctions
* Same configuration of tiles around each vertex


  .. image:: _static/images/pavage_semi.*
      :width: 60%
      :align: center

Lattice Encoding
----------------

**Square lattice**

* Lattice points:  `\mathbb{Z}^2`:math:, direct access to direct neighbors `(i\pm 1, j)`:math:, `(i,j\pm 1)`:math:

**Triangular grid**

* Lattice points: special encoding of lattice points to  `\mathbb{Z}^2`:math:, three direct neighbors (two local configurations when mapped to  `\mathbb{Z}^2`:math:)

**Hexagonal grid**


* Lattice points: special encoding of lattice points to  `\mathbb{Z}^2`:math:, six direct neighbors (two local configurations when mapped to  `\mathbb{Z}^2`:math:)


  .. image:: _static/images/voisins.*
      :width: 80%
      :align: center


Lattice Encoding (ctd.)
-----------------------

**Cubic grid**

Trivial

**FCC/BCC grid**

    .. math::
      (x,y,z) \text{ is generated by } V_{fcc} \Leftrightarrow (x,y,z)\in \mathbb{Z}^3,  x+y+z=0\, (mod\, 2)

    .. math::
      (x,y,z) \text{ is generated by } V_{bcc} \Leftrightarrow (x,y,z)\in \mathbb{Z}^3,  x=y=z\, (mod\, 2)

**Elongated grids**

* E.g. square/cubic grid with different resolutions
* `\Rightarrow`:math: Remapping `\mathbb{Z}^3\rightarrow \mathbb{R}^3`:math: on-the-fly


Fundamental Topology Elements
=============================

Adjacency relationships in the square/cubic grid
------------------------------------------------

**Combinatorial approach**

In 2D:

* *4-neighbors*: pixels sharing an edge `(i\pm 1, j)`:math: and `(i,j\pm 1)`:math:
* *8-neighbors*: pixels sharing an edge or a vertex `(i\pm 1, j\pm 1)`:math:

In 3D:

* *6-neighbors*: voxels sharing a face
* *18-neighbors*: voxels sharing a face or an edge
* *26-neighbors*: voxels  sharing a face, an edge or a vertex


**Topological approach**

   Two pixels/voxels are *(k)-adjacent* is the intersection of their (closed) cell is of dimension `k`:math:


Mixing all dimensions:

* 4-neighbor, 18-neighbor `\equiv`:math: (1)-adjacent
* 8-neighbor, 26-neighbor `\equiv`:math: (0)-adjacent
* 6-neighbor `\equiv`:math: (2)-adjacent


More definitions
----------------

**(k)-path**

A sequence of digital points `:\{p_i\}_{i=0\ldots n}`:math: is a *(k)-path* if for each point, `p_i`:math: is (k)-adjacent to `p_{i-1}`:math: (except for `i=0`:math:)



**(k)-arc**

A *(k)-arc* is a (k)-path such that each `p_i`:math: has exactly two (k)-adjacent neighbors (except for extremities)



**(k)-curve**


A *(k)-curve* is a (k)-arc such that `p_0 = p_n`:math:


**(k)-object**

A set S of digital point is a (k)-object iff for any pair of points, there exists a (k)-path in S

Illustrations
-------------

.. list-table::

  - * .. image:: _static/images/topo.*
           :width: 70%
           :align: center


    * .. image:: _static/images/topo2.*
            :width: 100%
            :align: center

Illustrations (ctd.)
--------------------

.. image:: _static/images/canard_plein.*
            :width: 60%
            :align: center


Can you spot (k)-arcs/(k)-objects/(k)-curves for `k=\{0,1\}`:math: ?


Toward a definition of contour
------------------------------

**Objective**: define a notion of object contour/boundary matching with Jordan theory

* `C`:math: is a *Jordan curve* (or simple closed curve) in `\mathbb{R}^2`:math: if `C`:math: is the image of a continuous and injective map from the circle to `\mathbb{R}^2`:math:

**Jordan theorem** states that:

- `\mathbb{R}^2\setminus C`:math: has two connected components, one is bounded (aka interior) and the other one is unbounded (exterior)
- Each continuous path `\pi`:math: from an interior point to an exterior one crosses `C`:math: (with an odd number of intersections)
- Implies an orientation of `C`:math:


.. image:: _static/images/jordan.*
            :width: 60%
            :align: center


*Idea*  mimic a digital version of Jordan framework replacing `C`:math: by a (k)-curve ?


Digital paradox
---------------

Given the following (0)- and (1)-curves, do they define Jordan-like curve ?

.. container:: build animation

  .. image:: _static/images/jordan2D_1.*
        :width: 60%

  .. image:: _static/images/jordan2D.*
        :width: 60%

  `\Rightarrow`:math: **It depends.... we need a pair of adjacency relationships !**


Example: Filling holes
----------------------

.. image:: _static/images/remplissage.*
   :width: 100%
   :align: center


Adjacency pairs
---------------


`(\kappa,\lambda)`:math: **Jordan pair** such that *k* is the adjacency for the object and *l* the adjacency for the complementary

.. image:: _static/images/jordan2drepare.*
       :width: 70%
       :align: center

**In dimension 2**

   (0,1) and (1,0)

**In dimension 3**

   (2,1), (2,0) (1,2) and (0,2)


Border definition
-----------------

**Border**: Given a `(\kappa,\lambda)`:math: Jordan pair, the border of `X`:math: is the set of `(\kappa)`:math: -adjacent digital points which are `(\lambda)`:math: -adjacent to points in `X^C`:math:

* The result is a `(\kappa)`:math: -object but we need more constraints to have a `(\kappa)`:math: -curve
* Hard to generalize to 3D
* We do not have `\partial X=  X\setminus X^C`:math: (or kind of, both are considered as open sets)


.. list-table::

  * - .. image:: _static/images/bubble-object-border1.png
           :width: 100%

    - .. image:: _static/images/bubble-object-color-borders-48.png
           :width: 100%




Cellular grid space and topology
--------------------------------

**Idea** embed the digital space `\mathbb{Z}^n`:math: into a cellular space (cartesian cubic space) to represent oriented inter-pixel elements

**In 2D**

* 0-cells are called pointels (element of dimension 0), by convention, Digital points in `\mathbb{Z}^n`:math: are embedded into 0-cells
* 1-cells are called linels (element of dimension 1)
* 2-cells are called pixels
* each cell can be signed

**In nD**

* 0-, ... , n-cells
* by convention: n-cells are called *spels* and (n-1)-cells are called *surfels*

.. image:: _static/images/ctopo-1.png
     :width: 30%
     :align: center

(two 0-cells, two 2-cells and four 1-cells)

Digital Surface
---------------

**Principle** defines digital surface as a set of (n-1)-cells (surfels)


* Let us consider a `\beta`:math: relationship on surfels (anti-reflexive,  local transitive closure, locally defined)
* Given a `(\kappa,\lambda)`:math: Jordan adjacency pair, `(\kappa,\lambda,\beta)`:math:  triplet  is a Jordan triplet

 - `\beta`:math: is anti-reflexive
 - `\beta`:math: is a relationship on surfels
 - `\beta`:math: can  extract all surfels (informally)


**We can demonstrate that such Jordan triplets leads to well-defined digital Jordan surface**

*Illustration in 2D* (here, k=1)


.. image:: _static/images/digital-surface-IntAdjacency.png
        :width: 60%
        :align: center


Approach is valid for various digital structures

`\beta`:math: in 3D
-------------------

Two valid `\beta`:math: relationships on (2,1)- or (2,0)- pairs on closed objects

.. list-table::

  * - .. image:: _static/images/digital-surface-SurfaceTracking2.png
             :width: 40%
             :align: center

    - .. image:: _static/images/digital-surface-SurfaceTracking.png
            :width: 40%
            :align: center


`\beta`:math: relationship  + graph traversal (depth first, breadth first,...) `\Rightarrow`:math: digital surface tracker



.. list-table::

  * - .. image:: _static/images/suivi-parcours-largeur.png
             :width: 80%
             :align: center

    - .. image:: _static/images/suivi-artzy.png
            :width: 80%
            :align: center


*Efficiency of the tracker is guided by the `\beta`:math: complexity*


Generic Breadth-first tracker
-----------------------------
 .. image:: _static/images/algoHerman.png
            :width: 80%
            :align: center


For (2)-object

* `\beta`:math: is not oriented, each surfel is processed 4 times
* `\beta^*`:math: with oriented arcs (2 arcs per surfel), each surfel is processed 2 times
* `\beta^{*+}`:math: with oriented arcs (1 or 2 arcs per surfels), each surfel is processed 4/3 times (on average)

* **The graph is 4-regular**
* `\Rightarrow`:math: Hamiltonian path exists if `X`:math: is homeomorphic to a ball


Digital Surface Extraction
--------------------------


**Overall algorithm** (for single connected surface)

* Scan the image until we find a  first surfel
* Apply the tracker to traverse all surfels

.. image:: _static/images/digital-surface-bfv-all.png
     :width: 100%
     :align: center



**Complex Objects**

Several connected components, holes, ...

`\Rightarrow`:math: Scan the complete volume, mark all surfels  as potential starting surfels and apply the tracker on each starting surfel (removing traversed surfels)


Digitization schemes
====================

Main ideas
----------


**Formalize the embedding** `\mathbb{R}^n\rightarrow\mathbb{Z}^n`:math:

* To be able to generate digital objects by *digitization* of Euclidean ones
* Important if we want to propagate properties (roughly, the digitization of a Jordan curve should be a `(\kappa,\lambda)`:math:-  Jordan for some grid steps)
* When we define a differential estimator (e.g. curvature) on digital contour, allows us to design multigrid convergent estimators
* ...


Gauss model
-----------

Let `\mathcal{X}\subset \mathbb{R}^n`:math: and `X`:math: its *digitization*

    .. math::
        X = \mathcal{X}\cap\mathbb{Z}^n


  .. image:: _static/images/discGauss.png
      :width: 30%
      :align: center

* Easy to implement
* Mostly used on objects with 2-measure `\neq`:math: 0 **but** even in this case, `X`:math: may be empty
* By definition  `X \subseteq \mathcal{X}`:math:
* We need more constraints on `\mathcal{X}`:math: to ensure topological properties on `X`:math: or `\partial X`:math:

Gauss models (bis)
------------------

This model was first used to approximate

   .. math::
      \int_\mathcal{X} ds

by

   .. math::
      |X|



Grid intersection models
------------------------

**Idea** Defined for oriented contours `\partial\mathcal{X}`:math:

   For each intersection  `\partial\mathcal{X}`:math: with a grid edge, we *select* the {closer,inner,outer} grid point


(resp. GIQ -Grid Intersect Quantization-, OBQ -Object Boundary Quantization-, BBQ -Background Boundary Quantization-)


 .. image:: _static/images/discGrids.png
      :width: 30%
      :align: center


* We construct (0)-objects which could also be (0)-arcs or (0)-curves
* Less generic than Gauss model
* *bubbles* can appear on ties (when `\partial\mathcal{X}`:math: crosses the edge at its mid-point) `\Rightarrow`:math: global Oracle to remove ties
* Distance properties between `X`:math: and `\partial\mathcal{X}`:math:


Analytic models
---------------

**Generic definition**

Let  `d_*`:math: be a metric, `B`:math: its unit ball and `M=\check{B}`:math:

  .. math::
     \mathbb{A}(\mathcal{X})&=\{p\in\mathbb{Z}^n~|~ B(p)\cap \mathcal{X} \neq \emptyset\}
            \\&=\{p\in\mathbb{Z}^n~|~ d_*(p,\mathcal{X})\leq \frac{1}{2} \} \\&=(\mathcal{X}\oplus M)\cap\mathbb{Z}^n

  .. image:: _static/images/modele_analytique.png
      :align: center
      :width: 100%


Still *bubbles* may exist

  .. image:: _static/images/modele_analytique_generique.png
      :align: center
      :width: 60%


Properties
----------

Following the definition (F,G `\in \mathbb{R}^n`:math: ):



.. admonition:: prop.

   .. math::
      \mathbb{A}(F\cup G)=  \mathbb{A}(F) \cup  \mathbb{A}(G)

   .. math::
        \mathbb{A}(F)= \bigcup_{p\in F} \mathbb{A}(p)

   .. math::
        \mathbb{A}(F\cap G)\subseteq  \mathbb{A}(F) \cap \mathbb{A}(G)

   .. math::
        \text{if } F\subseteq G\text{ then }  \mathbb{A}(F) \subseteq \mathbb{A}(G)


`\Rightarrow`:math: **Allows modeling of digital objects but CSG approach** *(Constructive Solid Geometry)*


Interesting theoretical tool: multigrid digitization
----------------------------------------------------


**Idea** Digitization parametrized by a grid step

E.g. for Gauss digitization

    .. math::
         X_h = \left (\frac{1}{h}\cdot \mathcal{X}\right )\cap \mathbb{Z}^n

    .. image:: _static/images/resolution.*
        :width: 60%
        :align: center



Mathematical results can be obtained with constraints on `\mathcal{X}`:math:, for example


.. admonition:: thm.

    If `\partial \mathcal{X}`:math: is `C^2`:math: with bounded curvature, there exists a grid step `h_0`:math: such that for   `0<h<h_0`:math:, `X_h`:math: is *topologically equivalent* to `\mathcal{X}`:math:


.. admonition:: thm.


    If `\partial \mathcal{X}`:math: is `C^2`:math: with bounded curvature, the retro-projection from `\hat{x}\in\partial X_h`:math: onto `\partial \mathcal{X}`:math: at `x`:math: along its normal direction is *continuous*, *mono-valuated* and *surjective* (for  `0<h<h_0`:math:) and `\| \hat{x} -x\|_\infty \le h`:math:)


Another example
---------------

.. container:: build animation

  **Question 1** Given a digital object, How to estimate its  areas ?

  **Answer** Well, let's count the number of grid points (unit squares) (estimator denoted E)


  **Question 2** Is this estimator multigrid convergent ? What is the convergence speed ?

  **Answer**

  * Let's consider the estimator `E_h`:math: at grid-step h defined on the digitization of the Euclidean shape  `\mathcal{X}`:math: from a given class of shapes
  * If `\mathcal{X}`:math: is a finite convex shape, there exists a grid step `h_0`:math: such that for `0<h<h_0`:math: we have:

       .. math::
          | E_h( X_h ) - \mu(\mathcal{X}) | \leq O(h)

  [Gauss, Dirichlet]

  * If `\mathcal{X}`:math: is `C^3`:math: (or finitely piece-wise `C^3`:math: with positive curvature almost everywhere...) then

        .. math::
           | E_h( X_h ) - \mu(\mathcal{X}) | \leq O(h^{\frac{15}{11}+\epsilon})

    [Huxley,...]


  *Would there be better approaches ?*

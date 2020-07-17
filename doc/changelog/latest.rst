[latest]
========

Release Notes
-------------
Implement the ``W_I`` and ``W_II`` method for approximating exponentials of an MPO with an MPO, and MPS compression /
MPO application to an MPS, to allow time evolution with :meth:`~tenpy.algorithms.mpo_evolution.ExpMPOEvolution`.

Changelog
---------

Backwards incompatible changes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
- Remove argument `leg0` from :class:`~tenpy.networks.mpo.MPOGraph.build_MPO`.
- Remove argument `leg0` from :class:`~tenpy.networks.mpo.MPO.from_grids`, instead optionally give *all* `legs` as argument.
- Moved/renamed the module :mod:`tenpy.algorithms.mps_sweeps` to :mod:`tenpy.algorithms.mps_common`.
  The old `mps_sweeps` still exists for compatibility, but raises a warning upon import.



Added
^^^^^
- :class:`~tenpy.algorithms.mps_common.VariationalCompression` and
  :class:`~tenpy.algorithms.mps_common.VariationalApplyMPO` for variational compression
- Argument `insert_all_id` for :meth:`tenpy.networks.mpo.MPOGraph.from_terms` and :meth:`~tenpy.networks.mpo.MPOGraph.from_term_list`
- implemented the :class:`~tenpy.models.lattice.IrregularLattice`.
- extended user guide on lattices, :doc:`/intro/lattices`.


Changed
^^^^^^^
- By default, for an usual MPO define `IdL` and `IdR` on all bonds. This can generate "dead ends" in the MPO graph of
  finite systems, but it is useful for the `make_WI`/`make_WII` for MPO-exponentiation.
- :meth:`tenpy.models.lattice.Lattice.plot_basis` now allows to shade the unit cell and shift the origin of the plotted basis.
- Don't use `bc_shift` in :meth:`tenpy.models.lattice.Lattice.plot_couplings` any more - it lead to confusing figures.
  Instead, the new keyword `wrap=True` allows to directly connect all sites.
  This is done to avoid confusing in combination with :meth:`~tenpy.models.lattice.Lattice.plot_bc_identified`.

Fixed
^^^^^
- Wrong results of :meth:`tenpy.networks.mps.MPS.get_total_charge` with ``only_physical_legs=True``.
- :meth:`tenpy.models.lattice.Lattice.plot_bc_identified` had a sign error for the `bc_shift`.
- :meth:`~tenpy.models.lattie.Lattice.calc_H_MPO_from_bond` didn't work for charges with blocks > 1.
- TEBD: keep qtotal of the B tensors constant

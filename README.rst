Biopython package definitions for the Galaxy Tool Shed
======================================================

For an introduction to the Biopython Project, please see
http://biopython.org - and for an introduction to the
Galaxy Project, please see http://galaxyproject.org/

The Galaxy web platform is extensible allowing addition of
new tools to a Galaxy instance. These tools are shared via
a Galaxy Tool Shed, primarily http://toolshed.g2.bx.psu.edu
and the Test Tool Shed http://testtoolshed.g2.bx.psu.edu

In addition to new tools, the Galaxy Tool Shed also includes
software package definitions for use as dependencies. This
repository is for the development of the Biopython package
definitions shared on the main Tool Shed and Test Tool Shed:

* http://toolshed.g2.bx.psu.edu/view/biopython/
* http://testtoolshed.g2.bx.psu.edu/view/biopython/

Note that each release of Biopython gets its own predicatably
named entry on the Tool Shed, so that tools using Biopython
can specify the exact version of Biopython required. This is
important for reproducibility which is a Galaxy design goal.


Instructions for Galaxy Tool Authors
====================================

If you are writing a Galaxy Tool which uses a Python script
dependent on Biopython, in order for the Galaxy Tool Shed to
automatically install Biopython you must include a
``repository_dependencies.xml`` file declaring this as a
dependency, e.g.::

  <?xml version="1.0"?>
  <repositories description="Requires Biopython as a dependency.">
    <repository name="package_biopython_1_65" owner="biopython" />
  </repositories>

Also, in your tool XML file(s) you must include::

  <requirements>
    <requirement type="package" version="1.65">biopython</requirement>
  </requirements>

This will work on the main Tool Shed or the Test Tool Shed where
it will refer to these packages:

* http://toolshed.g2.bx.psu.edu/view/biopython/package_biopython_1_65
* http://testtoolshed.g2.bx.psu.edu/view/biopython/package_biopython_1_65

Since it is a compile time requirement, the Biopython package
itself will depend on NumPy, so you do not need to also declare
that as an explicit dependency.

However, the package will not trigger the installation of optional
packages such as ReportLab, MatPlotLib or NetworkX which parts of
Biopython require.

So, if for example you are writing a Galaxy tool in Python using
Biopython, MatPlotLib and SciPy you must explicitly declare them all
as dependencies in your ``repository_dependencies.xml`` file, e.g.::

  <?xml version="1.0"?>
  <repositories description="Requires Biopython, MatPlotLib and SciPy.">
    <repository name="package_biopython_1_65" owner="biopython" />
    <repository name="package_matplotlib_1_2" owner="iuc" />
    <repository name="package_scipy_0_14" owner="iuc" />
  </repositories>

And in your tool XML file(s) you would include::

  <requirements>
    <requirement type="package" version="1.65">biopython</requirement>
    <requirement type="package" version="1.4">matplotlib</requirement>
    <requirement type="package" version="0.14">scipy</requirement>
  </requirements>

This will work on the main Tool Shed refering to these packages
(and similarly on the Test Tool Shed):

* http://toolshed.g2.bx.psu.edu/view/biopython/package_biopython_1_65
* http://toolshed.g2.bx.psu.edu/view/iuc/package_matplotlib_1_4
* http://toolshed.g2.bx.psu.edu/view/iuc/package_scipy_0_14

These additional dependencies are maintained by the IUC, or in full
the "Intergalactic Utilities Commission" which is the tongue-in-cheek
name of the Galaxy Tool Shed review team, see:
http://wiki.galaxyproject.org/ReviewingToolShedRepositories

When looking for how to add further dependencies, search the Tool Shed
for "Tool dependency definitions", and in particular look for those
from the IUC:

* http://toolshed.g2.bx.psu.edu/view/iuc/
* http://testtoolshed.g2.bx.psu.edu/view/iuc/

In addition to the examples above, the following are of particular
relevance:

* https://testtoolshed.g2.bx.psu.edu/view/iuc/package_python_reportlab_3_1_44
* https://testtoolshed.g2.bx.psu.edu/view/iuc/package_networkx_1_9

For full details on how to define dependencies on the Galaxy Tool Shed,
see http://wiki.galaxyproject.org/DefiningRepositoryDependencies

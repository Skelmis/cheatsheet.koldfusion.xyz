Pypi
====

Uploading to Pypi
-----------------

1. Bump the version number but dont change anything else in setup.py
2. Delete the following directories if they exist. ``build``, ``project_name.egg-info``, ``dist``
3. Install ``wheel`` if required, ``pip install wheel``
4. Run ``python setup.py sdist bdist_wheel``
5. Run ``python -m twine upload ./dist/*`` and follow the instructions

Classifiers
-----------

Can never find the f*ckers when I need them

Find em `here <https://pypi.org/classifiers/>`_

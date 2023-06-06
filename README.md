# 7.Package-Open-Source-PyTorch-Extension-for-Multiple-CUDA-and-Python-Versions
We'd like to use GroundingDINO as a dependency in another open source project we are working on. But, to publish on PyPi, cross-platform wheels (built with manylinux) are needed and are not provided. 

Problem Description
We'd like to use GroundingDINO as a dependency in another open source project we are working on. But, to publish on PyPi, cross-platform wheels (built with manylinux) are needed and are not provided. GroundingDINO has C++ and CUDA code (located in groundingdino/models/GroundingDINO/csrc) which needs to be compiled and linked to the versions of PyTorch and CUDA that match the user's machine.

While we can build groundingdino at runtime, we haven't been able to get it to build and deploy properly to PyPi yet.

Acceptance Criteria
Delivery of code that builds wheel files that run with GPU acceleration and are deployable to PyPi that meet the following criteria:

Support Python 3.7, 3.8, 3.9, 3.10, 3.11
Support PyTorch 1.10, 1.11, 1.12, 1.13, 2.0
Support CUDA 10.2, 11.3, 11.6, 11.7, 11.8, 12.0, 12.1
Support Microarchitectures 6.0-9.0 (Pascal to Hopper)
A PyPi package loaded in a notebook demonstrating that it works.

Technical Details
As test cases, the following should work with GPU in Google Colab and other environments:

!pip install groundingdino_YOURFORK
import torch
from groundingdino import _C

As should this:

from groundingdino.util.inference import Model

Supplemental Resources
This PyTorch discussion thread: https://github.com/pytorch/builder/issues/468
This torch-extension-builder repo: https://github.com/charliebudd/torch-extension-builder (which I couldn't get to work all the way through)
My torch-extension-builder fork which does build the their test extension (using a self-hosted runner) but produces wheels with errors for GroundingDINO
The rf_groundingdino pip package which was outputted by my forked torch-extension-builder but throws this error when trying to load:
import torch
from groundingdino import _C

---------------------------------------------------------------------------
ImportError                               Traceback (most recent call last)
/tmp/ipykernel_11713/727891918.py in <module>
----> 1 from groundingdino import _C
ImportError: libc10-09ae2961.so: cannot open shared object file: No such file or directory

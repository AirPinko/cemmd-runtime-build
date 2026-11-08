# CemMD dependency runtime build

This repository contains only a workflow and documentation for converting the public CemMD Linux dependency image into a prebuilt SIF for AsterFire Go. It contains no CemMD application source, research data, user files, or credentials.

The source image is pinned to `ghcr.io/airpinko/cemmd-science-runtime@sha256:a145bd2fa7dadab62e96962a2821301f585cf6279e0f56dcd4487a122f785f4b`. The workflow does not check out the application repository.

The workflow uses a standard Ubuntu GitHub-hosted runner. It installs Apptainer from the project's official signed Ubuntu repository and records the installed version, converts the immutable image with gzip compression, checks Python dependencies in an isolated network-disabled container, and verifies the SIF hash inside the transport image.

The transport image is `ghcr.io/airpinko/cemmd-runtime-build:1.0.0-sif`. Its `/sif/cemmd-science_1.0.0.sif` layout follows the [official AsterFire image guide](https://sidereus-ai.feishu.cn/wiki/BZcYwmIb3imqqQkpU7kcKMhynbh).

The workflow uses the job-scoped GitHub token only for its package push. It does not execute Packmol or LAMMPS. Successful conversion proves packaging and dependency availability, not platform deployment or scientific validation.

Dependency licenses remain in the source runtime image. Workflow runs publish validation metadata as an artifact. Inspect the latest run result before using an image tag; the presence of this repository alone does not mean a build succeeded.


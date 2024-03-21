# BSP S2: Development and maintenance of an open-source project

This repository contains all important information about Bachelor's semester project in Semester 2, performed during Spring 2023 by Fedor Chikhachev, under the supervision of Dr. Alfredo Capozucca.

## Project report

A formal [report](BSP-S2-open-source-report.pdf) in University's designated format has been produced as a final deliverable for this project.

## Source code

All files with the code are contained inside `.github/workflows` folder. There are several CI scripts, which performs a synchronisation workflow between 2 repositories, private and public. `biginteger` folder contains a C++ library, which simulates an existing project with the corresponding `tests.yml` workflow in `.github/workflows`.

For the moment the code available here is working only for the specific pair of repositories ([sync-repos-public](https://github.com/FChikh/sync_repos_public) and [sync-repos-private](https://github.com/FChikh/sync_repos_private)), as some parts of code are related concretely to these repositories (e.g. their source addresses and API tokens with corresponding access rights). The access to these repositories is personal, as they contain some private information. So it is unavailable for the moment to probide a live demonstration for everybody. To see this software in action, please refer to video demonstrations in ST-VIDEO deliverable.

Also, this repository contains draft versions of `LICENSE`, `CODE_OF_CONDUCT`, `CONTRIBUTING` files for [E4L project](https://e4l.uni.lu), as they were produced as a part of research.

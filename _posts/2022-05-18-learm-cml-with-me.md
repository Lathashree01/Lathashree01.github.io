---
layout: post
title: Learn CML with me
subtitle: Excerpt from Soulshaping by Jeff Brown
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
tags: [machine learning]
author: Lathashree Harisha
---

Continuous Machine Learning (CML) is an open-source tool that helps implement CI/CD style integration in the development of Machine Learning Models. CML helps evaluate different approaches and givesa visual report to make wiser decisions based on the criteria we set. The key file for CML to work is `.github/workflows/cml.yaml`

Below is an example of how a `cml.yaml` file looks like:

~~~
name: CML
on: [push]
jobs:
  train-and-report:
    runs-on: ubuntu-latest
    container: docker://ghcr.io/iterative/cml:0-dvc2-base1
    steps:
      - uses: actions/checkout@v3
      - name: Train model
        env:
          REPO_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        run: |
          pip install -r requirements.txt
          python train.py  # generate plot.png

          # Create CML report
          cat metrics.txt >> report.md
          echo '![](./plot.png "Confusion Matrix")' >> report.md
          cml comment create report.md
~~~

* sample file taken from one of the CML example repos

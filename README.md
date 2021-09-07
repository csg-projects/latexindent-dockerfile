# Latexindent Dockerfile

A lightweight dockerfile for the latexindent plugin.

----------

[Latexindent.pl](https://github.com/cmhughes/latexindent.pl) is a great perl script to automatically indent `LaTeX` files.
On Linux, it ships with the `texlive` distribution.
Unfortunately, it only comes with `texlive-full` which is 5 GB in size.

In this dockerfile I have packaged the minimal dependencies to run the script without a `LaTeX` distribution.
Note that this means that you won't be able to compile within, just check the format.
It is particularly useful for CI/CD settings in which a certain style must be reinforced.
It can easily be embedded in an existing job (e.g. GH Action) as follows:
```yaml
jobs:
  check-format:
    runs-on: ubuntu-20.04 
    container: csegarragonz/latexindent:0.0.1
    steps:
      # --- Check out code ---
      - uses: actions/checkout@v2
      # --- Formatting checks ---
      - name: "LaTeX format Check"
        run: latexindent *.tex
      - name: "Test if format is compliant"
        run: git diff --exit-code
```

---------

The image is publicly available in [Docker Hub](https://hub.docker.com/repository/docker/csegarragonz/latexindent).
PRs are welcome.

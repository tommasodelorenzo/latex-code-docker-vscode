# Write Latex documentation with interactive code using Docker and VSCode

A Docker container for [`Latex`](https://www.latex-project.org/) in `VSCode`. The base image is [Latex Dev Container](https://github.com/qdm12/latexdevcontainer).

## Installation
1. Clone the repo.
2. Launch VSCode.
3. Open a new remote connection, and choose `open folder in container`.
4. Choose the cloned folder.

This will `build` and `run` the container, starting a remore `VSCode` session inside the container. The whole project's folder is mounted as a volume (see `./.devcontainer/docker-compose`) to persist every edit.

For more info about using `VSCode` in Docker containers see [this link](https://code.visualstudio.com/docs/remote/containers).

## Usage
Once the session is started, create a folder with a `.tex` file inside, and start typing.
Every `.tex` document is compiled authomatically every time it is saved.

For a brief intro to `Latex` see [this link](https://it.overleaf.com/learn/latex/Learn_LaTeX_in_30_minutes).

### Useful packages

As per December 2022, `Latex Dev Container` installs the full version of [`Tex Live 2021`](https://tug.org/texlive/) containing almost every package you would need. To add additional packages, just add them in `./devcontainer/Dockerfile` below `RUN tlmgr install` and run `rebuild container`.

Here is a list of additional packages already present in the Dockerfile.

- [`pythontex`](https://github.com/gpoore/pythontex): to excecute `python` code in `Latex` for an interactive documentation. As one would expect, `pythontex` has `python` as requirement: here `python3.9` is installed.

    **Pythontex usage example**
    ```
    \newcommand{\pymultiply}[2]{\py{#1*#2}}

    \begin{pycode}
        print("Python says ``Hello!''")
    \end{pycode}

    $8 \times 256 = \pymultiply{8}{256}$
    ```

- [`minted`](https://it.overleaf.com/learn/latex/Code_Highlighting_with_minted): for fancy and customizable code visualization.

    **Minted usage example**
    ```
    \begin{minted}[mathescape,
        linenos,
        numbersep=5pt,
        gobble=2,
        frame=lines,
        framesep=2mm]{csharp}
    string title = "This is a Unicode $\pi$ in the sky"
    /*
    Defined as $\pi=\lim_{n\to\infty}\frac{P_n}{d}$ where $P$ is the perimeter
    of an $n$-sided regular polygon circumscribing a
    circle of diameter $d$.
    */
    const double pi = 3.1415926535
    \end{minted}
    ```

## Requirements
1. [VSCode](https://code.visualstudio.com/)
    - Extension [`remote-containers`](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
1. [Docker e Docker-compose](https://docs.docker.com/)

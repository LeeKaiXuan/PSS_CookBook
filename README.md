# PSS_CookBook
Documentation for introducing the usage of PSS language.

# Setup (Local Builder)
If you need to generate the website locally, please install MkDocs first. (Reference: https://squidfunk.github.io/mkdocs-material/getting-started/)<br>
I recommend using docker if you develop on Microsoft Windows (e.g., win10/win11).

Steps of setup docker:
1. Download and install [Docker Desktop](https://www.docker.com/).
2. In Docker Desktop, search `squidfunk/mkdocs-material` on the top console then pull it.
3. Clone this repo to a local directory.
4. Go to the directory, and create a text file named `Dockerfile` without any extension.
5. Paste the following context into `Dockerfile`:
```Dockerfile
FROM squidfunk/mkdocs-material
RUN pip install mkdocs-macros-plugin
RUN pip install mkdocs-glightbox
RUN pip install mkdocs-git-revision-date-localized-plugin
```
6. Run PowerShell at the current path and enter following command:
```bash
docker build -t squidfunk/mkdocs-material .
```
7. The older docker image can be deleted.

# Previewing on Docker
Run a PowerShell inside the local repo with following command:
```bash
docker run --rm -it -p 8000:8000 -v .:/docs squidfunk/mkdocs-material
```
Once local MkDocs' server is ready, run another PowerShell with following command:
```bash
docker run --rm -it -v .:/docs squidfunk/mkdocs-material build
```
After the site is built, you can preview it on ```http://localhost:8000/```

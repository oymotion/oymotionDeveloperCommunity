# OYMotion Community Web Site

The web site [https://oymotion.github.io](https://oymotion.github.io) is built upon [mkDocs](www.mkdocs.org)

## How to contribute

* Install [mkDocs](http://www.mkdocs.org)

```BASH
pip install mkdocs
```

Please refer to [How to Install mkdocs](http://www.mkdocs.org/#installation)

* Install required theme

```BASH
pip install mkdocs-material
```

* Make some changes

```BASH
git clone https://github.com/oymotion/oymotionDeveloperCommunity.git
cd oymotionDeveloperCommunity
...(make some changes)
mkdocs serve
```

*note* mkdocs.exe can be found in "%LOCALAPPDATA%\Packages\PythonSoftwareFoundation.Python.3.10_*\LocalCache\local-packages\Python310\Scripts" on Windows.

Then you would be able to preview the web page at [http://localhost:8000](http://localhost:8000)

## How to Update web site as [oymotion](https://oymotion.github.io) owner

* Install [mkDocs](http://www.mkdocs.org)

```BASH
pip install mkdocs
```

Please refer to [How to Install mkdocs](http://www.mkdocs.org/#installation)

* Deploying Docs

```BASH
git clone https://github.com/oymotion/oymotionDeveloperCommunity.git
git remote add oymotionIO https://github.com/oymotion/oymotion.github.io.git
cd oymotionDeveloperCommunity
...(merge pull request or make some changes by yourself)
mkdocs gh-deploy
git checkout gh-pages
git push oymotionIO gh-pages:master
```

> **Note:** You should never edit any files in `oymotion.github.io` repository and
`gh-pages` branch  by hand otherwise you will lose your work.

For more details about `mkdocs gh-deploy`,please refer to [How to Deploying Docs](http://www.mkdocs.org/user-guide/deploying-your-docs/)

# OYMotion Community Web Site
This web site(https://oymotion.github.io) is built upon [mkDocs](www.mkdocs.org)

## How to contribute
### Install [mkDocs](http://www.mkdocs.org) 

Please reference [How to Install mkdocs](http://www.mkdocs.org/#installation)

### Make some changes

```
$ git clone https://github.com/oymotion/communitySite.git
$ cd websiit
$ ...(make some changes)
$ mkdocs serve
```
Then you would be able to preview you local web site at http://localhost:8000

## How to Update web site as [oymotion](https://oymotion.github.io) owner

### Install [mkDocs](http://www.mkdocs.org) 
Please reference [How to Install mkdocs](http://www.mkdocs.org/#installation)

### Deploying Docs

```
$ git clone https://github.com/oymotion/communitySite.git
$ git remote add oymotionIO https://github.com/oymotion/oymotion.github.io.git
$ cd websit
$ ...(merge pull request or make some changes by yourself)
$ mkdocs gh-deploy
$ git checkout gh-pages
$ git push oymotionIO gh-pages:master
```
**Note:** You should never edit andy files in `oymotion.github.io` repository and
`gh-pages` branch  by hand otherwise you will lose your work.

For more details about `mkdocs gh-deploy`,please reference [How to Deploying Docs](http://www.mkdocs.org/user-guide/deploying-your-docs/)


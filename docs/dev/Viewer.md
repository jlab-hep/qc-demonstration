# 1. Introduction
The Viewer is a beautiful and convenient web interface for LocalDB.

We can:
* check data
* register module/chip (under construct)
* sync (not implemented yet)


# 2. Getting start
## a) download
```
git clone https://github.com/jlab-hep/localDB-tools.git
cd localDB-tools/viewer
./setup_viewer.sh
```

## b) configure
Edit `localDB-tools/viewer/conf.yml` as your setup.

(You can copy it from `localDB-tools/scripts/yaml/web-conf.yml`)

![viewer_configure](https://github.com/jlab-hep/localDB-tools/blob/devel/docs/images/viewer_configure.png)


# 3. Usage
```
$ cd localDB-tools/viewer
$ python app.py --config conf.yml
```

![viewer_app](https://github.com/jlab-hep/localDB-tools/blob/devel/docs/images/viewer_app.png)

type "http://127.0.0.1:5000/localdb/" in browser to check the viewer

(ref : [installation](https://github.com/jlab-hep/Yarr/wiki/Web-interface)/Advance)
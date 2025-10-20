# Building

To build **francis** you'll need to follow the workspace setup instruction available [here](https://github.com/Mord3rca/repo-workspace?tab=readme-ov-file#setup)

TL;DR - In a empty dir, do:
```sh
repo init -u ssh://git@github.com/Mord3rca/manifests
repo sync -j4
```

Right after that, just run `make francis` and your image will be in *output/francis/images/sdcard.img*

# Storage

All users have 10GB of persistent storage during the course in `/home/jovyan`,
and they can all use `/tmp` for some extra scratch space.

## Notebooks for tutorials

As an instructor you probably have some notebooks that you want to provide to
users. Please add those to the GitHub repository
[neurohackademy/nh2021-curriculum](https://github.com/neurohackademy/nh2021-curriculum)
and refer to Ariel Rokem (@arokem) for guidance about this.

The material in the GitHub repository neurohackademy/nh2021-curriculum will be
synced to `/nh/curriculum` every five minutes, which anyone can access in a
read-only manner.

During startup of the user environment, each users will get a read/write copy of
`/nh/curriculum` merged to `~/curriculum` in a a manner described [in more
detail
here](https://jupyterhub.github.io/nbgitpuller/topic/automatic-merging.html).

if you as an instructor made recent changes to the GitHub repository, those will
be seen in `/nh/curriculum` quickly within 5 minutes, but changes in
`~/curriculum` will be seen only after the user restarts their environment using
the JupyterLab File menu under the menu item `Hub control panel`.

## Datasets for tutorials

If you want to provide datasets to the participants using the notebooks, there
are some options to consider. Please feel free to discuss your options with Erik
Sundell (@consideRatio) or open a GitHub issue about your considerations.

### Datasets in a git repository (neurohackademy/nh2021-curriculum)

It is an option to put the datasets next to the notebooks on GitHub. It will
make the GitHub repository a bit larger though. I would advice to avoid this for
anything close to or larger than 10MB. It can make the git repository used by
everyone slower to download and work with even if you delete the file later
because its now part of git history.

### Datasets on the internet

It is an option to put the dataset on internet somewhere. A consideration to
make is what will happen if hundreds of participants download a ~100MB file
simultaneously from a server though. A server could get overloaded or block
access thinking it was suspicious that it received so many sudden download
requests.

The internet connection will be extremely good for the participants though.

### Datasets in the Docker image

Another options is to embed the dataset in the Docker image. I think this could
be a sensible option for datasets of the size ~1GB. A downside is that the image
gets slow to build and download, but if the data is to be made available anyhow,
its quite efficient to download it as part of the Docker image once for each
server which may have ~40 users on it.

### Datasets in shared network attached storage

Both instructors and participants will have access to shared network attached
storage mounted in `/nh/data` or `~/data` which is is a symlink to `/nh/data`..
Anything an instructor writes there will be available in a read-only mode for
participants. While this is practical, it is not well tested at scale and could
bottleneck.

How efficient would it become if hundreds of users accessed this simultaneously
and they all wanted to read hundreds a gigabyte of data? If you choose this
option, I suggest a backup solution is considered alongside it.

```{note}
Remember that participants will access `/nh/data` or `~/data` which is is a
symlink to `/nh/data`. in a read-only mode!
```

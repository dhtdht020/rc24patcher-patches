# RiiConnect24 Patcher Patches

This is the repository used by the cross platform python RiiConnect24 Patcher (Work In Progress) to obtain updated patches from the internet.
**Warning: This is a README discussing unreleased software, it might change in the future.**


## .patch Files

RiiConnect24 Patcher uses [bsdiff4](https://github.com/ilanschnell/bsdiff4) for diff and delta encoding, these files are used by the following function to apply patches to WAD files obtained from NUS:

    patch(title_id, patch_file)

## Creating .patch files

RiiConnect24 Patcher will have an interactive patch creation wizard that will walk you through the process, but for now- you can directly use bsdiff4:

    import bsdiff4
    
    bbsdiff4.file_diff('wad_from_nus.wad', 'modified
    _wad.wad', 'patch_file.patch')

## Directory structure of .patch file host

By default, the patcher uses this GitHub repository to obtain patches through the function obtain_online_patch

    obtain_online_patch(name, region, version, hostname)

This is the currect expected / recommended structure of the host:
```
.
├── checkmiiout                        # name
│   ├── EU                             # region
│   │   ├── latest                     # version
│   │   │   ├── checkmiiout.patch      # name.patch
│   │   │   └── checkmiiout.json       # name.json
│   │   ├── beta                       # version
│   │   └── v1            	           # version
│   ├── US                             # region
│   └── JP                             # region
└── README.md
```
I'm considering having the version directory be above the region, we'll see.

## Patch JSON

JSONs are not implemented yet- and there's no clear structure, but they will soon be used by the patcher to obtain the following information:

 - Title ID
 - Title Version
 - Latest update date

## Regions

Regions can be everything, and are called by the patcher by string.
The recommended names are:

 - EU: PAL patches (Europe)
 - US: NTSC-U patches (United States)
 - JP: NTSC-J patches (Japan)

The region directories should contain version directories.

## Versions

Versions are used by the patcher exclusively for the ability to store multiple variations of a patch under the same name and region.

By default, the patcher uses the version "latest", making it mandatory.

Examples of usage are "beta", "version2", "test".

Version directories should include:

    ├── name.patch         # .patch file
    └── name.json          # JSON file

## Contributing
Feel free to submit an issue or a PR, if anything seems to be missing or if you are interested in providing a new patch.
# RiiConnect24 Patcher Patches

This is the repository used by the cross platform python RiiConnect24 Patcher (Work In Progress) to obtain updated patches from the internet.

**Warning: This is a README discussing unreleased software, it might change in the future.**


## .patch Files

RiiConnect24 Patcher uses [bsdiff4](https://github.com/ilanschnell/bsdiff4) for diff and delta encoding, these files are used by the following function to apply patches to WAD files obtained from NUS:

    patch(title_id, patch_file)

## Creating .patch Files

RiiConnect24 Patcher will have an interactive patch creation wizard that will walk you through the process, but for now- you can directly use bsdiff4:

    import bsdiff4
    
    bbsdiff4.file_diff('wad_from_nus.wad', 'modified_wad.wad', 'patch_file.patch')

## Directory structure of .patch file host

By default, the patcher uses this GitHub repository to obtain patches through the function obtain_online_patch

    obtain_online_patch(name, region, hostname)

    http://hostname/name/region/

This is the currect expected / recommended structure of the host:
#### Example Directory Structure:
```
.
├── checkmiiout                        # name
│   ├── EU                             # region
│   │   ├── checkmiiout.patch          # name.patch (Patch File)
│   │   ├── checkmiiout.json           # name.json  (JSON)
│   │   └── cetk                       # Ticket File
│   ├── US                             # region
│   ├── JP                             # region
│   └── ALL                            # region
│   contents.json                      # contents of repo
│   LICENSE
└── README.md
```
I'm considering having the version directory be above the region, we'll see.

## JSON Configuration Files

Configuration files are used to give the patcher information on the title id and additional steps that are required for the patch.

These files will be generated automatically by the patcher's planned patch creation assist.

Configs are not finalized yet- and there's no clear structure, but they will soon be used by the patcher to obtain the following information:

 - Title ID
 - Display Name
 - Version
 - Additional steps
 - Description about the patch and further information
 - Support URL and email
 - Patch metadata

Currently, those are the supported objects:

 - display_name - Optional, but recommended. In case this is missing, the patcher will use a fallback name.
 - title_id - ID of the title to be obtained from NUS and patched. (Required)
 - title_version - Version of the title to be obtained from NUS and patched. (Required)
 - grab_ticket - If a ticket should be grabbed from this repository instead of NUS.
 - region - Region / Version in the repository. This should be the same as the name of the region directory (e.g EU, ALL, Beta)
 - name - Patch Name in the repository. This should be the same as the name of the patch directory (e.g checkmiiout)
### Example configuration JSON:
    {
    "display_name":"Check Mii Out Channel (Europe)",
    "title_id":"0001000148415050",
    "title_version":"512",
    "grab_ticket":"true",
    "region":"EU",
    "name":"checkmiiout"
    }

## Regions (Also Versions)


Regions can be everything, and are called by the patcher by string.
The recommended names are:

 - EU: PAL patches (Europe)
 - US: NTSC-U patches (United States)
 - JP: NTSC-J patches (Japan)
 - ALL: Region free patches

Regions can also be used for different versions and variations of the patch, examples for versions are:

 - Beta
 - Test

Region directories should include:

    ├── name.patch       # .patch file
    ├── name.json        # .json file
    └── name.cetk        # in case a ticket is needed


## Ticket
Most titles don't have their ticket on NUS, so this is often required to properly decrypt NUS contents.

To use the ticket, add the following to the title JSON:

    {
	  "grab_ticket":"true"
    }

## contents.json
The contents file will be used to create a proper list of available patches in the patcher, and provide information about the host and what it includes.

This is currently unused.

## Contributing
Feel free to submit an issue or a PR, if anything seems to be missing or if you are interested in providing a new patch.
# TD Style Guide

A mostly reasonable approach to Touch Designer Development

this document was started and heavily inspired by the Gamemakin ue-style guide and represents the collected insights 7+ years of daily freelance TD development by @picturesbyrobots. The techniques herein were codified, battle tested, documented, and refined while the former served as creative technologist at the never estabilshed, always innovative,  @radicalmedia 

## Table of Contents



## Important Terminology

---
<a name="td"></a>
##### td
TD stands for Touch Designer. A platform for visual thinking. 

<a name="toe-patch"></a>
##### toe/.toe/patch

The word `toe` or `patch` is used interchangeably to refer to the entire Touch Designer project contained within a specefic `repo` this can be made up of any combination of external scripts, tox modules, assets, e.t.c 

<a name="tox"></a>
##### tox

the word `tox` refers to a submodule within a larger TD patch. Toxes can be made from containers by right clicking and selecting save as external tox.

<a name="extension"></a>
##### extension

TD allows for any COMP to have a custom python class added to it to extend it's functionality. This allows containers for a bunch of neato tricks that helps to make the final touch designer project a little less fragile and easier to version control. 

<a name="COMP"></a>
##### COMP
A comp is a container operator. these are gray operators in the network pane and usually contain other nodes

<a name="cases"></a>
##### Cases


There are a few different ways you can `CaseWordsWhenNaming`. Here are some common casing types:

> ###### PascalCase
>
> Capitalize every word and remove all spaces, e.g. `DesertEagle`, `StyleGuide`, `ASeriesOfWords`.
>
> ###### camelCase
>
> The first letter is always lowercase but every following word starts with uppercase, e.g. `desertEagle`, `styleGuide`, `aSeriesOfWords`.
>
> ###### Snake_case
>
> Words can arbitrarily start upper or lowercase but words are separated by an underscore, e.g. `desert_Eagle`, `Style_Guide`, `a_Series_of_Words`.


<br>



<a name="-1"></a>
## 1. Principles

--- 

<a name="-1."></a>
### 1.1 If your TD project already has a style guide, you should follow it
If you are working on a project or with a team that has a pre-existing style guide, it should be respected.  Any inconsistency between an existing style guide and this guide should defer to the existing.

Style guides should be living documents. You should propose style guide changes to an existing style guide as well as this guide if you feel the change benefits all usages.  

Try not to argue to much about cases. As long as it's consisitent it truly doesn't matter. 

<br>

> #### "Arguments over style are pointless. There should be a style guide, and you should follow it."
> [_Rebecca Murphey_](https://rmurphey.com)

<br>

<a name="-1.2"></a>
### 1.2 All structure, assets, and code in any TD project should look like a single person created it, no matter how many people contributed  
<br>

Moving from one project to another should not cause a re-learning of style and structure. Conforming to a style guide removes unneeded guesswork and ambiguities. This is especially true in large scale TD driven installations, where there might be many patches that span multiple rooms or activations. Similary, mainting and enforcing a TD style at the organization level ensures that when patches are revisted for remounts or reactivations there is a minimum amount of re-learing or re-remembering of which specefic style was used at this part of the project. This is especially crucial in the many segments in which TD is appropriate given the sometimes limited time frames for a project

<a name="-1.3"></a>
### 1.3 Style is for teams. Sometimes that team is past and future you 
<br> 

Following a consistent style is also helpful if you are revisting a past patch that you made for a project four years ago. It means that it will take less time to get up to speed with what past you was trying to accomplish with a specefic patch. This will make things easier and you can get to upgrading to the latest coolest sensor without having to remember where you put that render module.

<a name="-1.4"></a>
### 1.4 Be respectful of other peoples work.
it's a nice thing to do to mention or leave a comment if possible if you're adapting or implementing a specefic technique that you picked up from watching a YouTube tutorial or read about in the forums. You never know who might open your patch one day. 


<br>

<a name="anc"></a>
<a name="0"></a>
# 0. Naming Conventions  

<a name="0.1-operators"></a>
## 0.1 Operators
All Network operators should have a unified case. this can either be snake case. as in `select_raster_config` or camel as in `selectRasterConfig` The organization or team should pick a style and stick with it. 

This guide thinks that using `snake_case` for operators is a slightly more optimal approach. Extensions and User Parameters in TD are required to start with a `Capital Letter` thus it's easy for other team members to quickly visualy identify potentially interesting or added parameters. Consider `op.config.IsStart` vs `op('movie_file_in').par.file`  Knowing that the project uses snake case the TD author can assume that the property `IsStart` is a custom element added by a team member.

### 0.1.2 Operator Names  
In general one should try to rename most operators in a chain to give a reader the sense of what they do. This is helpful because when another developer is looking at an expression or a reference in a seperate part of your network they can get a sense of your intentions. This is especially true of `null` operators at the end of a chain.  Consider the difference between seeing a reference to `../../../config/null5` in a select CHOP vs `op.config.op('computed_rasters')` 




<a name="0.2-External Text Files"></a>
## 0.2 External Text Files

### 0.2.1 Extensions
External files that are used as the source code for extensions should be prefixed with the project abbreviation and titled in `CamelCase` For example a source file that makes a container behave like a Movie Player for a project called `BlueParadox` might be called `BPMoviePlayerEXT.py` or `BPMoviePlayer.py`

### 0.2.2 Shaders
External files as the source code for glsl or geo shaders should follow the same syntax as the operator that it's referencing so a glsl top called `particles_velocity_update` might have a shader associated with it called `particle_update.glsl`



# 1.0 Project Directory Structure


There are multiple ways to organize a content project directory structure. This guide uses a style that emphasizes clear visibility when viewing the project if the file explorer and in the repository. In general this structure provides the following benefits:

- provide an unambigous entry point to the project
- easily searchable based on asset type
- general compatibility with folder dats
- makes source control via git less of a pain


## 1e1 Example Project Directory Structure
<pre>
    |-- <a href="#2.2">Project Name</a>
        <a href="#1.2">|-- .gitignore</a>
        <a href="#1.1">|-- main.toe    </a>
        |-- subprocess1.toe
        <a href="#1.4">|-- subprocess2.toe</a>
        |-- setup.bat
        <a href="#1.3">|-- config.json</a>
        <a href="#1.5">|-- src</a>
        |   |-- scripts
        |   |   |-- py
        |   |   |   |-- SomeExtensionNameEXT.py
        |   |   |-- glsl
        |   |   |   |-- particles_update.frag
        |   |-- <a href="#1.6">tox</a>
        |   |   |-- raster_template.tox
        |-- <a href="#1.7">assets</a>
        |   |-- binaries
        |   |   |-- dlls
        |   |   |-- exe
        |   |-- mov
        |   |-- img
        |   |-- ref
        |   |-- data
</pre>



<a name="1.1"></a>
<a name="main.toe"></a>
## The main `toe` file should be clearly delinated.
The main entry point of the TD project should be clearly delinated at the project directory level. This file should be the first one a new developer opens when getting started with the project. On all projects we like to use `main.toe` as the top level file name. Backups in TD should be either disabled (this is what version control is for ) or should be configured to be saved into a Backup folder.

<a name="1.2"></a>
<a name=".gitignore"></a>
## Use a `.gitignore` to keep large files out of your repo.
`HAP` or `NOTCH` files are great for playback. Unfortuneatly, these files can get VERY large. Ideally you should use .gitignore to ignore all files in the `mov` directory to keep them out of the project. On cloning the repo a combination of .bat scripts and or manual copying from seperate distro links should be use to get the file up to speed. Ideally the projects `README.md` will have project and or organization specefic guidelines on how a new developer can go about getting content files



<a name="1.3"></a>
<a name="config.json"></a>
## Use an external configuration file to setup project specefic variables
If the project is planned for multiple deployments with machine specefic variables it's good practice to use a `config.json` file to store these configurations on a per-machine basis. Ideally the team will combine this with <a href="#3.1">3.1</a> to make deployment onto production hardware a little less painful. An incomplete list of some of these variables might entail:
<pre>
- external server IPs
- Serial port designations
- monitor configuration
- Spout sender and receiver names
- Hardware identifiers
- e.t.c.
</pre>

Ideally this file is ignored in version control and it's the responsibility of `main.toe` to create one if it doesn't exist. This can combine with `#4.1` to allow for machine specefic calibration during the deployment phase.





<a name="1.4"></a>
<a name="external toes"></a>
## Keep External subprocess `toe` files at the top level of the project

Sometimes it's necessary to split certain parts of a TD patch out into an external subprocess to be launched from `main.toe` with the addition of the `Engine COMP` in newer version of Touch this has become less neccessary when dealing with certain IO considerations. However, if your project reliese on more than one TD process these `toe` files should be stored in the top level of the project to make sure that references to external assets and source files don't break. 


<a name="1.5"></a>
<a name="src folder"></a>
## Wherever possible try to externalize source scripts in an external file

This is important. By default many TD modules will store external scripts in memory. This will make source control extremely difficult. Externalize large project specefic modules, extensions, shaders, and scripts early and reference them using relative paths. i.e. `src/scripts/py/SomeGreatEXT.py` not `C:\Users\Dave\Touch\PROJECT\script` By enforcing this early and often the team or organization will benefit from conventional source control tools. Some easy canididates for externalization include 
<pre>
- any and all extensions
- mission critical material and glsl TOP sources
- Script CHOP,TOP,and DAT sources
- modules and module libs
- http DAT or TCP dat callbacks
</pre>

Obvs this is not a hard and fast rule. If you're dropping a one liner into a `TimerChop` callback that you probably don't need to externalize it. If you're writing what's essentially a webserver based on a HTTP callback then you might think about it. In theory you could also consider putting that logic into an <a href="#3.2">Extension</a>


<a name ="1.6"></a>
<a name ="external toxes"></a>
## Keep important networks externalized and versioned

Related to <a href="#1.5">1.5</a> and <a href="#3.1">3.1</a> The team should try and keep all top level toxes externalized and version controlled. This will essentially allow different team members to work in tandem on different aspects of the project without the fear of overwriting each other's work when it comes to merge time. Tops can be externalized via the `Common` tab. Use a relative path here to prevent deployment hell


<a name ="1.7"></a>
<a name ="local assets"></a>
## All assets should be referenced via relative paths
Many projects will rely on a set of external assets to function properly. All assets referenced by `main.toe` should be kept in a sub folder called `assets` and referenced with relative paths. This will prevent missing files when the patch is migrated from the developers local environment to production hardware. see <a href="#3.3"> 3.3 </a> for a detailed discussion of file import practices.


# 2.0 TD Networks
This section will focus on the internal composition of TD Networks and their internals.

<a name = "2.1"></a>
<a name = "Compiling"></a>
## 2.1 Compiling
-   All operators, scripts, and networks should compile with zero warnings and zero errors. If a script or TOX throws a compile error it should be corrected or mitagated as quickly as possible, regardless of whether or not it effects the functionality of the patch,
-   **do not** submit networks, toxes, or scripts to source control. When another developer opens the patch they will not be able to know for certain if the broken error is mission critical or has been ignored due to loose code style requirements


<a name = "2.2"></a>
<a name = "network topology"></a>
## 2.2 Network Topology
The top level of a network is the first thing a new developer or user sees when they open your patch. Where possible the top level of a TD project should contain only `containers` or `bases` that have been clearly named based on its function. 

todo : image here

This allows the next developer to quickly gain a high level understanding of the core functions of your patch and allows them to get up to speed on their tasks quickly. If possible, each of these top level containers is an external tox and stored in version control

<a name = "2.3"></a>
<a name = "Global operator shortcuts"></a>

## 2.3 Use Global Operator Shortcuts for Top Level Containers.

related to the above. Every container at the top level of the project can and should be assigned a global operator shortcut. 

> This will cut down greatly on references breaking over the course of developement and allow for some neat tricks. For example: a container that is responsible for running some post processing effects on a raster generated by a `render` network start it's chain with a `SelectTOP` that uses an expression with the reference `op.render.op('final')` this allows multiple developers to work in tandem on different aspects of the project without the added burden of merging top level networks or worse, having networks over written by conflicting versions of the same project.


<a name = "2.4"></a>
<a name = "config"></a>
## 2.3 Store project specefic variables in a `config` base

All variables referenced in many different places in the networks should be stored in a top level base named `config` 


While the specefic type of variables will vary by project some good canidates for this technique include:
<pre>
- project resolution.
- server uris
- replicator counts
- content folder paths
- specefic asset dimensions
</pre>

### 2.3.1 Assign a `global operator shortcut` to the `config` base
When referencing the project level `config` top use `expressions` to keep your networks clean. `global operator shortcuts` can configured in the `Common` pane of the network operator. 
> This allows you to reference the project configuration anywhere in the project without having to break your references. Consider the following:

image


vs:


image

> while both approaches can lead to the correct project resolution. If this variable is hard coded into multiple operators accross many different networks this can lead to unexpected behavior in the case of updates or scope changes.





# 3.0 Development
The following section focuses on a set of development practices. Mileage may vary based on team composition and project time frame.

























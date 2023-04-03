# TD Style Guide

A mostly reasonable approach to Touch Designer Development

this document was started and heavily inspired by the Gamemakin ue-style guide, represents the collected insights 7+ years of daily freelance TD development by @picturesbyrobots. the techniques herein were codified, battle tested, documented, and refined while the former served as creative technologist at the never estabilshed, always innovative,  @radicalmedia 

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



# 0.1 Project Directory Structure


There are multiple ways to organize a content project directory structure. This guide uses a style that emphasizes clear visibility when viewing the project if the file explorer and in the repository. In general this structure provides the following benefits:

- provide an unambigous entry point to the project
- easily searchable based on asset type
- general compatibility with folder dats
- makes source control via git less of a pain


## 1e1 Example Project Directory Structure
<pre>
    |-- <a href="#2.2">Project Name</a>
        |-- .gitignore
        |-- main.toe
        |-- subprocess1.toe
        |-- subprocess2.toe
        |-- config.json
        |-- src
        |   |-- scripts
        |   |   |-- py
        |   |   |   |-- SomeExtensionNameEXT.py
        |   |   |-- glsl
        |   |   |   |-- particles_update.frag
        |   |-- tox
        |   |   |-- raster_template.tox
        |-- binaries
        |   |-- dlls
        |   |-- exe
        |-- assets
        |   |-- mov
        |   |-- img
        |   |-- ref
        |   |-- data
</pre>










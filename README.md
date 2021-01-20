# Unity Style Guide

This article contains ideas for setting up a projects structure and a naming convention for scripts and assets in Unity.

<a name="toc"></a>
## Table of Contents

> 1. [Introduction](#introduction)
> 1. [Project Structure](#structure)
> 1. [Scripts](#scripts)
> 1. [Asset Naming Conventions](#anc)
> 1. [Asset Workflows](#asset-workflows)

<a name="introduction"></a>
## 1. Introduction

### Sections

> 1.1 [Style](#style)

> 1.2 [Important Terminology](#importantterminology)

<a name="style"></a>
### 1.1 Style

#### If your project already has a style guide, you should follow it.
If you are working on a project or with a team that has a pre-existing style guide, it should be respected.  Any inconsistency between an existing style guide and this guide should defer to the existing.

Style guides should be living documents however and you should propose style guide changes to an existing style guide as well as this guide if you feel the change benefits all usages.

> ##### *Arguments over style are pointless. There should be a style guide, and you should follow it.*
> [_Rebecca Murphey_](https://rmurphey.com)

#### All structure, assets, and code in any project should look like a single person created it, no matter how many people contributed.
Moving from one project to another should not cause a re-learning of style and structure. Conforming to a style guide removes unneeded guesswork and ambiguities.

It also allows for more productive creation and maintenance as one does not need to think about style, simply follow instructions. This style guide is written with best practices in mind, meaning that by following this style guide you will also minimize hard to track issues.

#### Friends do not let friends have bad style.
If you see someone working either against a style guide or no style guide, try to correct them.

When working within a team or discussing within a community, it is far easier to help and to ask for help when people are consistent. Nobody likes to help untangle someone's spaghetti code or deal with assets with names they can't understand.

If you are helping someone who's work conforms to a different but consistent and sane style guide, you should be able to adapt to it. If they do not conform to any style guide, please direct them here.

<a name="importantterminology"></a>
### 1.2 Important Terminology

<a name="terms-prefab"></a>
#### Prefabs
Unity uses the term Prefab for a system that allows you to create, configure, and store a GameObject complete with all its components, property values, and child GameObjects as a reusable Asset.

<a name="terms-level-map"></a>
#### Levels/Maps/Scene
Levels refer to what some people call maps or what Unity calls Scenes. A level contains a collection of objects.

<a name="terms-serializable"></a>
#### Serializable
Variables that are Serializable are shown in the Inspector window in Unity. For more information see Unity's documentation on [Serializable](https://docs.unity3d.com/Manual/script-Serialization.html).

<a name="terms-cases"></a>
#### Cases
There are a few different ways you can name things. Here are some common casing types:

> ##### PascalCase
> Capitalize every word and remove all spaces, e.g. `DesertEagle`, `StyleGuide`, `ASeriesOfWords`.
> 
> ##### camelCase
> The first letter is always lowercase but every following word starts with uppercase, e.g. `desertEagle`, `styleGuide`, `aSeriesOfWords`.
>  ##### lowercase
> All letters are lowercase, e.g. `deserteagle`, 
>
> ##### Snake_case
> Words can arbitrarily start upper or lowercase but words are separated by an underscore, e.g. `desert_Eagle`, `Style_Guide`, `a_Series_of_Words`.

**[⬆ Back to Top](#table-of-contents)**

<a name="structure"></a>
## 2. Project Structure
The directory structure style of a project should be considered law. Asset naming conventions and content directory structure go hand in hand, and a violation of either causes unneeded chaos.

In this style, we will be using a structure that relies more on filtering and search abilities of the Project Window for those working with assets to find assets of a specific type instead of another common structure that groups asset types with folders.

> Using a prefix [naming convention](#asset-name-modifiers), using folders to contain assets of similar types such as `Meshes`, `Textures`, and `Materials` is a redundant practice as asset types are already both sorted by prefix as well as able to be filtered in the content browser.
<pre>
Assets
    <a name="#structure-developers">_Developers</a>(Use a `_`to keep this folder at the top)
        DeveloperName
            (Work in progress assets)
    <a name="structure-top-level">ProjectName</a>
            Characters
            	Anakin
            FX
                Vehicles
                    Abilities
                        IonCannon
                            (Particle Systems, Textures)
                Weapons
            Gameplay
                Characters
                Equipment
                Input
                Vehicles
                    Abilities
                    Air
                        TieFighter
                            (Models, Textures, Materials, Prefabs)
            <a name="#structure-levels">_Levels</a>
                Frontend
                Act1
                    Level1
            Lighting
                HDRI
                Lut
                Textures
            MaterialLibrary
            	Debug
            	Shaders
            Objects
                Architecture (Single use big objects)
                    DeathStar
                Props (Repeating objects to fill a level)
                    ObjectSets
                        DeathStar
            Scripts
                AI
                Gameplay
                    Input
                Tools
            Sound
                Characters
                Vehicles
                    TieFighter
                        Abilities
                            Afterburners
                Weapons
            UI
                Art
                    Buttons
                Resources
                    Fonts
    ExpansionPack (DLC)
    Plugins
    ThirdPartySDK  
</pre>




The reasons for this structure are listed in the following sub-sections.

### Sections

> 2.1 [Folder Names](#structure-folder-names)

> 2.2 [Top-Level Folders](#structure-top-level)

> 2.3 [Developer Folders](#structure-developers)

> 2.4 [Levels](#levels)

> 2.5 [Define Ownership](#structure-ownership)

> 2.6 [`Assets` and `AssetTypes`](#structure-assettypes)

> 2.7 [Large Sets](#structure-large-sets)

> 2.8 [Material Library](#structure-material-library)

> 2.9 [Scene Structure](#scene-structure)


<a name="2.1"></a>
<a name="structure-folder-names"><a>
### 2.1 Folder Names
These are common rules for naming any folder in the content structure.

<a name="2.1.1"></a>
#### Always Use [PascalCase](#terms-cases)
PascalCase refers to starting a name with a capital letter and then instead of using spaces, every following word also starts with a capital letter. For example, `DesertEagle`, `RocketPistol`, and `ASeriesOfWords`.

<a name="2.1.2"></a>
#### Never Use Spaces
Re-enforcing [2.1.1](#2.1.1), never use spaces. Spaces can cause various engineering tools and batch processes to fail. Ideally your project's root also contains no spaces and is located somewhere such as `D:\Project` instead of `C:\Users\My Name\My Documents\Unity Projects`.

<a name="2.1.3"></a>
#### Never Use Unicode Characters And Other Symbols
If one of your game characters is named 'Zoë', its folder name should be `Zoe`. Unicode characters can be worse than [Spaces](#2.1.2) for engineering tools and some parts applications don't support Unicode characters in paths either.

Related to this, if your project has and your computer's user name has a Unicode character (i.e. your name is `Zoë`), any project located in your `My Documents` folder will suffer from this issue. Often simply moving your project to something like `D:\Project` will fix these mysterious issues.

Using other characters outside `a-z`, `A-Z`, and `0-9` such as `@`, `-`, `_`, `,`, `*`, and `#` can also lead to unexpected and hard to track issues on other platforms, source control, and weaker engineering tools. 

<a name="structure-no-empty-folders"></a>
#### No Empty Folders
There simply shouldn't be any empty folders. They clutter the content browser.

If you find that the content browser has an empty folder you can't delete, you should perform the following:
1. Be sure you're using source control.
1. Navigate to the folder on-disk and delete the assets inside.
1. Close the editor.
1. Make sure your source control state is in sync (i.e. if using Perforce, run a Reconcile Offline Work on your content directory)
1. Open the editor. Confirm everything still works as expected. If it doesn't, revert, figure out what went wrong, and try again.
1. Ensure the folder is now gone.
1. Submit changes to source control.

<a name="2.2"></a>
<a name="structure-top-level"><a>
### 2.2 Use A Top Level Folder For Project Specific Assets
All of a project's assets should exist in a folder named after the project. For example, if your project is named 'Generic Shooter', _all_ of it's content should exist in `Assets/GenericShooter`.

> The `Developers` folder is not for assets that your project relies on and therefore is not project specific. See [Developer Folders](#2.3) for details about this.

There are multiple reasons for this approach.

<a name="2.2.1"></a>
#### No Global Assets
Often in code style guides it is written that you should not pollute the global namespace and this follows the same principle. When assets are allowed to exist outside of a project folder it often becomes much harder to enforce a strict structure layout as assets not in a folder encourages the bad behavior of not having to organize assets.

Every asset should have a purpose, otherwise it does not belong in a project. If an asset is an experimental test and shouldn't be used by the project it should be put in a [`Developer`](#2.3) folder.

<a name="2.2.2"></a>
#### Reduce Migration Conflicts
When working on multiple projects it is common for a team to copy assets from one project to another if they have made something useful for both. 

By placing all project specific assets in a top level folder you reduce the chance of migration conflict when importing those assets into a new project.

<a name="2.2.2e1"></a>
##### Master Material Example
For example, say you created a master material in one project that you would like to use in another project so you migrated that asset over. If this asset is not in a top level folder, it may have a name like `Assets/MaterialLibrary/M_Master`. If the target project doesn't have a master material already, this should work without issue.

As work on one or both projects progress their respective master materials may change to be tailored for their specific projects due to the course of normal development.

The issue comes when, for example, an artist for one project created a nice generic modular set of static meshes and someone wants to include that set of static meshes in the second project. If the artist who created the assets used material instances based on `Assets/MaterialLibrary/M_Master` as they're instructed to, when a migration is performed there is a great chance of conflict for the previously migrated `Assets/MaterialLibrary/M_Master` asset.

This issue can be hard to predict and hard to account for. The person migrating the static meshes may not be the same person who is familiar with the development of both project's master material, and they may not be even aware that the static meshes in question rely on material instances which then rely on the master material. The Migrate tool requires the entire chain of dependencies to work however, and so it will be forced to grab `Assets/MaterialLibrary/M_Master` when it copies these assets to the other project and it will overwrite the existing asset.

It is at this point where if the master materials for both projects are incompatible in _any way_, you risk breaking possibly the entire material library for a project as well as any other dependencies that may have already been migrated, simply because assets were not stored in a top level folder. The simple migration of static meshes now becomes a very ugly task.

<a name="2.2.3"></a>
#### Samples, Templates, and 3rd Party Content Are Risk-Free
An extension to [2.2.2](#2.2.2), if a team member decides to add sample content, template files, or assets they bought from a 3rd party, it is guaranteed that these new assets will not interfere with the project in any way unless your project's top level folder is not uniquely named.

You can not trust 3rd party content to fully conform to the [top level folder rule](#2.2). There exist many assets that have the majority of their content in a top level folder but also have possibly modified Unity sample content as well as level files polluting the global `Assets` folder.

When adhering to [2.2](#2.2), the worst 3rd party conflict you can have is if two 3rd party assets both have the same sample content. If all your assets are in a project specific folder, including sample content you may have moved into your folder, your project will never break.

#### DLC, Sub-Projects, and Patches Are Easily Maintained
If your project plans to release DLC or has multiple sub-projects associated with it that may either be migrated out or simply not cooked in a build, assets relating to these projects should have their own separate top level content folder. This make cooking DLC separate from main project content far easier. Sub-projects can also be migrated in and out with minimal effort. If you need to change a material of an asset or add some very specific asset override behavior in a patch, you can easily put these changes in a patch folder and work safely without the chance of breaking the core project.

<a name="2.3"></a>
<a name="structure-developers"></a>
### 2.3 Use Developers Folder For Local Testing
During a project's development, it is very common for team members to have a sort of 'sandbox' where they can experiment freely without risking the core project. Because this work may be ongoing, these team members may wish to put their assets on a project's source control server. Not all teams require use of Developer folders, but ones that do use them often run into a common problem with assets submitted to source control.

It is very easy for a team member to accidentally use assets that are not ready for use which will cause issues once those assets are removed. For example, an artist may be iterating on a modular set of static meshes and still working on getting their sizing and grid snapping correct. If a world builder sees these assets in the main project folder, they might use them all over a level not knowing they could be subject to incredible change and/or removal. This causes massive amounts of re-working by everyone on the team to resolve.

If these modular assets were placed in a Developer folder, the world builder should never of had a reason to use them and the whole issue would never happen.

Once the assets are ready for use, an artist simply has to move the assets into the project specific folder. This is essentially 'promoting' the assets from experimental to production.


<a name="levels"></a>
### 2.4 All [Scene](#terms-level-map) Files Belong In A Folder Called Levels
Level files are incredibly special and it is common for every project to have its own map naming system, especially if they work with sub-levels or streaming levels. No matter what system of map organization is in place for the specific project, all levels should belong in `Assets/ProjectNameName/Levels`.

Being able to tell someone to open a specific map without having to explain where it is is a great time saver and general 'quality of life' improvement. It is common for levels to be within sub-folders of `Levels`, such as `Levels/Campaign1/` or `Levels/Arenas`, but the most important thing here is that they all exist within `Assets/ProjectNameName/Levels`.

This also simplifies the job of cooking for engineers. Wrangling levels for a build process can be extremely frustrating if they have to dig through arbitrary folders for them. If a team's levels are all in one place, it is much harder to accidentally not cook a map in a build. It also simplifies lighting build scripts as well QA processes.

<a name="2.5"></a>
<a name="structure-ownership"></a>
### 2.5 Define Ownership
In teams of more than one, define ownership of zone/assets/features. Some assets like scenes or prefabs do not handle simultaneous changes by multiple people very well, creating conflict. Having a single person who can change (or give the right to change) a given assets helps to avoid that problem.

<a name="2.6"></a>
<a name="structure-assettypes"></a>
### 2.6 Do Not Create Folders Called `Assets` or `AssetTypes`

<a name="2.6.1"></a>
#### Creating a folder named `Assets` is redundant.
All assets are assets.

<a name="2.6.2"></a>
#### Creating a folder named `Meshes`, `Textures`, or `Materials` is redundant.
All asset names are named with their asset type in mind. These folders offer only redundant information and the use of these folders can easily be replaced with the robust and easy to use filtering system the Content Browser provides.

Want to view only static mesh in `Environment/Rocks/`? Simply turn on the Static Mesh filter. If all assets are named correctly, they will also be sorted in alphabetical order regardless of prefixes. Want to view both static meshes and skeletal meshes? Simply turn on both filters. this eliminates the need to potentially have to `Control-Click` select two folders in the Content Browser's tree view.

> This also extends the full path name of an asset for very little benefit. The `SM_` prefix for a static mesh is only three characters, whereas `Meshes/` is seven characters.

Not doing this also prevents the inevitability of someone putting a static mesh or a texture in a `Materials` folder.

<a name="2.7"></a>
<a name="structure-large-sets"></a>
### 2.7 Very Large Asset Sets Get Their Own Folder Layout

This can be seen as a pseudo-exception to [2.6](#2.6).

There are certain asset types that have a huge volume of related files where each asset has a unique purpose. The two most common are Animation and Audio assets. If you find yourself having 15+ of these assets that belong together, they should be together.

For example, animations that are shared across multiple characters should lay in `Characters/Common/Animations` and may have sub-folders such as `Locomotion` or `Cinematic`.

> This does not apply to assets like textures and materials. It is common for a `Rocks` folder to have a large amount of textures if there are a large amount of rocks, however these textures are generally only related to a few specific rocks and should be named appropriately. Even if these textures are part of a [Material Library](#2.8).

<a name="2.8"></a>
<a name="structure-material-library"></a>
### 2.8 `MaterialLibrary`

If your project makes use of master materials, layered materials, or any form of reusable materials or textures that do not belong to any subset of assets, these assets should be located in `Assets/ProjectName/MaterialLibrary`.

This way all 'global' materials have a place to live and are easily located.

> This also makes it incredibly easy to enforce a 'use material instances only' policy within a project. If all artists and assets should be using material instances, then the only regular material assets that should exist are within this folder. You can easily verify this by searching for base materials in any folder that isn't the `MaterialLibrary`.

The `MaterialLibrary` doesn't have to consist of purely materials. Shared utility textures, material functions, and other things of this nature should be stored here as well within folders that designate their intended purpose. For example, generic noise textures should be located in `MaterialLibrary/Utility`.

Any testing or debug materials should be within `MaterialLibrary/Debug`. This allows debug materials to be easily stripped from a project before shipping and makes it incredibly apparent if production assets are using them if reference errors are shown.

<a name="2.9"></a>
<a name="scene-structure"></a>
## 2.9 Scene Structure
Next to the project’s hierarchy, there’s also scene hierarchy. As before, we’ll present you a template. You can adjust it to your needs. Use named empty game objects as scene folders.

<pre>
Debug
Management
UI
Cameras
Lights
World
    Terrain
    Props
Gameplay
	Actors
	Items
_Dynamic
</pre>

 - All empty objects should be located at 0,0,0 with default rotation and scale.
 - For empty objects that are only containers for scripts, use “@” as prefix – e.g. @Cheats
 - When you’re instantiating an object in runtime, make sure to put it in _Dynamic – do not pollute the root of your hierarchy or you will find it difficult to navigate through it.

**[⬆ Back to Top](#table-of-contents)**

<a name="scripts"></a>

## 3. Scripts

This section will focus on C# classes and their internals. When possible, style rules conform to Microsoft's C# standard.

### Sections
> 3.1 [Class Organization](#classorganization)

> 3.2 [Compiling](#compiling)

> 3.3 [Variables](#variables)

> 3.4 [Functions](#functions)

<a name="classorganization"></a>
### 3.1 Class Organization
Source files should contain only one public type, although multiple internal classes are allowed.

Source files should be given the name of the public class in the file.

Organize namespaces with a clearly defined structure,

Class members should be alphabetized, and grouped into sections:
* Constant Fields
* Static Fields
* Fields
* Constructors
* Properties
* Events / Delegates
* LifeCycle Methods (Awake, OnEnable, OnDisable, OnDestroy)
* Public Methods
* Private Methods
* Nested types

Within each of these groups order by access:
* public
* internal
* protected
* private
```
namespace ProjectName
{
	/// <summary>  
	/// Brief summary of what the class does
	/// </summary>
    public class Account
    {
      #region Fields
      
      [Tooltip("Public variables set in the Inspector, should have a Tooltip")]
      public static string BankName;
      
	  /// <summary>  
	  /// They should also have a summary
	  /// </summary>
      public static decimal Reserves;
 
	  public string BankName;
	  public const string ShippingType = "DropShip";
	  
	  private float _timeToDie;
	  
	  #endregion
	  
	  #region Properties
	  
      public string Number {get; set;}
      public DateTime DateOpened {get; set;}
      public DateTime DateClosed {get; set;}
      public decimal Balance {get; set;}
            
	  #endregion
	 
	  #region LifeCycle
	  
      public Awake()
      {
        // ...
      }
      
      #endregion
	  #region Public Methods
	  
      public AddObjectToBank()
      {
        // ...
      }
      
      #endregion
    }
}
```

#### Script Templates
To save some time you can overwrite Unity's default script template with your own  to automatically setup the namespace and regions etc. See this Unity [support](https://support.unity3d.com/hc/en-us/articles/210223733-How-to-customize-Unity-script-templates) article to learn how.

<a name="namespace"></a>
#### Namespace
Use a namespace to ensure your scoping of classes/enum/interface/etc won't conflict with existing ones from other namespaces or the global namespace. The project should at minimum use the projects name for the Namespace to prevent conflicts with any imported Third Party assets.

#### All Public Functions Should Have A Summary

Simply, any function that has an access modifier of Public should have its summary filled out. 

```
/// <summary>
/// Fire a gun
/// </summary>
public void Fire()
{
// Fire the gun.
}
```

#### Foldout Groups
If a class has only a small number of variables, Foldout Groups are not required.

If a class has a moderate amount of variables (5-10), all [Serializable](#serializable) variables should have a non-default Foldout Group assigned. A common category is `Config`.

To create Foldout Groups there are 2 options in Unity. 

* The first is to define a `[Serializable] public Class` inside the main class however this can have a performance impact. This allows the use of the same variable name to be shared.
* The second option is to use the Foldout Group Attribute available with [Odin Inspector](https://odininspector.com/).

```
[[Serializable](https://docs.unity3d.com/ScriptReference/Serializable.html)]
public struct PlayerStats
	{
        public int MovementSpeed;
    }
    
[FoldoutGroup("Interactable")]
public int MovementSpeed = 1;
```

#### Commenting
Comments should be used to describe intention, algorithmic overview, and/or logical flow.
It would be ideal if from reading the comments alone someone other than the author could understand a function’s intended behavior and general operation.

While there are no minimum comment requirements and certainly some very small routines need no commenting at all, it is hoped that most routines will have comments reflecting the programmer’s intent and approach.

##### Comment Style
Place the comment on a separate line, not at the end of a line of code.

Begin comment text with an uppercase letter.

End comment text with a period.

Insert one space between the comment delimiter (//) and the comment text, as shown in the following example.

The // (two slashes) style of comment tags should be used in most situations. Where ever possible, place comments above the code instead of beside it. Here are some examples:
```
        // Sample comment above a variable.
        private int _myInt = 5;
```

#### Regions
The `#region` directive enables you to collapse and hide sections of code in C# files. The ability to hide code selectively makes your files more manageable and easier to read. 
```
#region "This is the code to be collapsed"
    Private components As System.ComponentModel.Container
#endregion
```

#### Spacing
Do use a single space after a comma between function arguments.

Example: `Console.In.Read(myChar, 0, 1);`
* Do not use a space after the parenthesis and function arguments.
* Do not use spaces between a function name and parenthesis.
* Do not use spaces inside brackets.
<a name="3.1"></a>
<a name="compiling"></a>
### 3.2 Compiling
All scripts should compile with zero warnings and zero errors. You should fix script warnings and errors immediately as they can quickly cascade into very scary unexpected behavior.

Do *not* submit broken scripts to source control. If you must store them on source control, shelve them instead.

### 3.3 Variables
The words `variable` and `property` may be used interchangeably.

#### Variable Naming

##### Nouns
All non-boolean variable names must be clear, unambiguous, and descriptive nouns. 

##### Case
All variables use PascalCase unless marked as [private](#privatevariables) which use camelCase. 

Use PascalCase for abbreviations of 4 characters or more (3 chars are both uppercase).

##### Considered Context
All variable names must not be redundant with their context as all variable references in the class will always have context.

###### Considered Context Examples:
Consider a Class called `PlayerCharacter`.

**Bad**

* `PlayerScore`
* `PlayerKills`
* `MyTargetPlayer`
* `MyCharacterName`
* `CharacterSkills`
* `ChosenCharacterSkin`

All of these variables are named redundantly. It is implied that the variable is representative of the `PlayerCharacter` it belongs to because it is `PlayerCharacter` that is defining these variables.

**Good**

* `Score`
* `Kills`
* `TargetPlayer`
* `Name`
* `Skills`
* `Skin`

#### Variable Access Level
In C#, variables have a concept of access level. Public means any code outside the class can access the variable. Protected means only the class and any child classes can access this variable internally. Private means only this class and no child classes can access this variable.
Variables should only be made public if necessary.

Prefer to use the attribute `[SerializeField]` instead of making a variable public.

##### Local Variables
Local variables should use camelCase.

###### Implicitly Typed Local Variables
Use implicit typing for local variables when the type of the variable is obvious from the right side of the assignment, or when the precise type is not important.
```
var var1 = "This is clearly a string.";
var var2 = 27;
var var3 = Convert.ToInt32(Console.ReadLine());
// Also used in for loops
for (var i = 0; i < bountyHunterFleets.Length; ++i) {};
```

Do not use var when the type is not apparent from the right side of the assignment.
Example
```
int var4 = ExampleClass.ResultSoFar();
```

<a name="privatevariables"></a>
##### Private Variables
Private variables should have a prefix with a underscore `_myVariable` and use camelCase.

Unless it is known that a variable should only be accessed within the class it is defined and never a child class, do not mark variables as private. Until variables are able to be marked `protected`, reserve private for when you absolutely know you want to restrict child class usage.

##### Do _Not_ use Hungarian notation
Do _not_ use Hungarian notation or any other type identification in identifiers
```
// Correct
int counter;
string name;
 
// Avoid
int iCounter;
string strName;
```

#### Variables accessible in the Editor

##### Tooltips 
All [Serializable](#serializable) variables should have a description in their `[Tooltip]` fields that explains how changing this value affects the behavior of the script.

##### Variable Slider And Value Ranges
All [Serializable](#serializable) variables should make use of slider and value ranges if there is ever a value that a variable should _not_ be set to.

Example: A script that generates fence posts might have an editable variable named `PostsCount` and a value of -1 would not make any sense. Use the range fields `[Range(min, max)]` to mark 0 as a minimum.

If an editable variable is used in a Construction Script, it should have a reasonable Slider Range defined so that someone can not accidentally assign it a large value that could crash the editor.

A Value Range only needs to be defined if the bounds of a value are known. While a Slider Range prevents accidental large number inputs, an undefined Value Range allows a user to specify a value outside the Slider Range that may be considered 'dangerous' but still valid.

#### Variable Types

##### Booleans

###### Boolean Prefix
All booleans should be named in PascalCase but prefixed with a verb.

Example: Use `isDead` and `hasItem`, **not** `Dead` and `Item`.

###### Boolean Names
All booleans should be named as descriptive adjectives when possible if representing general information.

Try to not use verbs such as `isRunning`. Verbs tend to lead to complex states.

###### Boolean Complex States
Do not use booleans to represent complex and/or dependent states. This makes state adding and removing complex and no longer easily readable. Use an enumeration instead.

Example: When defining a weapon, do **not** use `isReloading` and `isEquipping` if a weapon can't be both reloading and equipping. Define an enumeration named `WeaponState` and use a variable with this type named `WeaponState` instead. This makes it far easier to add new states to weapons.

##### Enums
Enums use PascalCase and use singular names for enums and their values. Exception: bit field enums should be plural. Enums can be placed outside the class space to provide global access.

Example: 
```
public enum WeaponType
{
    Knife,
    Gun
}

// Enum can have multiple values
[Flags]
public enum Dockings
{
	None = 0,
	Top = 1,
}

public WeaponType Weapon
```

##### Arrays
Arrays follow the same naming rules as above, but should be named as a plural noun.

Example: Use `Targets`, `Hats`, and `EnemyPlayers`, not `TargetList`, `HatArray`, `EnemyPlayerArray`.

##### Interfaces
Interfaces are led with a capital `I` then followed with PascalCase.

Example: ```public interface ICanEat { }```

<a name="functions"></a>
### 3.4 Functions, Events, and Event Dispatchers
This section describes how you should author functions, events, and event dispatchers. Everything that applies to functions also applies to events, unless otherwise noted.

#### Function Naming
The naming of functions, events, and event dispatchers is critically important. Based on the name alone, certain assumptions can be made about functions. For example:

* Is it a pure function?
* Is it fetching state information?
* Is it a handler?
* What is its purpose?

These questions and more can all be answered when functions are named appropriately.

<a name="function-verbrule"></a>
#### All Functions Should Be Verbs
All functions and events perform some form of action, whether its getting info, calculating data, or causing something to explode. Therefore, all functions should start with verbs. They should be worded in the present tense whenever possible. They should also have some context as to what they are doing.

Good examples:

* `Fire` - Good example if in a Character / Weapon class, as it has context. Bad if in a Barrel / Grass / any ambiguous class.
* `Jump` - Good example if in a Character class, otherwise, needs context.
* `Explode`
* `ReceiveMessage`
* `SortPlayerArray`
* `GetArmOffset`
* `GetCoordinates`
* `UpdateTransforms`
* `EnableBigHeadMode`
* `IsEnemy` - ["Is" is a verb.](http://writingexplained.org/is-is-a-verb)

Bad examples:

* `Dead` - Is Dead? Will deaden?
* `Rock`
* `ProcessData` - Ambiguous, these words mean nothing.
* `PlayerState` - Nouns are ambiguous.
* `Color` - Verb with no context, or ambiguous noun.

#### Functions Returning Bool Should Ask Questions
When writing a function that does not change the state of or modify any object and is purely for getting information, state, or computing a yes/no value, it should ask a question. This should also follow [the verb rule](#function-verbrule).

This is extremely important as if a question is not asked, it may be assumed that the function performs an action and is returning whether that action succeeded.

Good examples:

* `IsDead`
* `IsOnFire`
* `IsAlive`
* `IsSpeaking`
* `IsHavingAnExistentialCrisis`
* `IsVisible`
* `HasWeapon` - ["Has" is a verb.](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html)
* `WasCharging` - ["Was" is past-tense of "be".](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html) Use "was" when referring to 'previous frame' or 'previous state'.
* `CanReload` - ["Can" is a verb.](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html)

Bad examples:

* `Fire` - Is on fire? Will fire? Do fire?
* `OnFire` - Can be confused with event dispatcher for firing.
* `Dead` - Is dead? Will deaden?
* `Visibility` - Is visible? Set visibility? A description of flying conditions?

#### Event Handlers and Dispatchers Should Start With `On`
Any function that handles an event or dispatches an event should start with `On` and continue to follow [the verb rule](#function-verbrule).

Good examples:

* `OnDeath` - Common collocation in games
* `OnPickup`
* `OnReceiveMessage`
* `OnMessageRecieved`
* `OnTargetChanged`
* `OnClick`
* `OnLeave`

Bad examples:

* `OnData`
* `OnTarget`

**[⬆ Back to Top](#table-of-contents)**
<a name="anc"></a>
<a name="4"></a>

## 4. Asset Naming Conventions
Naming conventions should be treated as law. A project that conforms to a naming convention is able to have its assets managed, searched, parsed, and maintained with incredible ease.

Most things are prefixed with the prefix generally being an acronym of the asset type followed by an underscore.

**Assets use [PascalCase](#cases)**

<a name="base-asset-name"></a>
<a name="4.1"></a>
### 4.1 Base Asset Name - `Prefix_BaseAssetName_Variant_Suffix`
All assets should have a _Base Asset Name_. A Base Asset Name represents a logical grouping of related assets. Any asset that is part of this logical group 
should follow the the standard of  `Prefix_BaseAssetName_Variant_Suffix`.

Keeping the pattern `Prefix_BaseAssetName_Variant_Suffix` in mind and using common sense is generally enough to warrant good asset names. Here are some detailed rules regarding each element.

`Prefix` and `Suffix` are to be determined by the asset type through the following [Asset Name Modifier](#asset-name-modifiers) tables.

`BaseAssetName` should be determined by short and easily recognizable name related to the context of this group of assets. For example, if you had a character named Bob, all of Bob's assets would have the `BaseAssetName` of `Bob`.

For unique and specific variations of assets, `Variant` is either a short and easily recognizable name that represents logical grouping of assets that are a subset of an asset's base name. For example, if Bob had multiple skins these skins should still use `Bob` as the `BaseAssetName` but include a recognizable `Variant`. An 'Evil' skin would be referred to as `Bob_Evil` and a 'Retro' skin would be referred to as `Bob_Retro`.

For unique but generic variations of assets, `Variant` is a two digit number starting at `01`. For example, if you have an environment artist generating nondescript rocks, they would be named `Rock_01`, `Rock_02`, `Rock_03`, etc. Except for rare exceptions, you should never require a three digit variant number. If you have more than 100 assets, you should consider organizing them with different base names or using multiple variant names.

Depending on how your asset variants are made, you can chain together variant names. For example, if you are creating flooring assets for an Arch Viz project you should use the base name `Flooring` with chained variants such as `Flooring_Marble_01`, `Flooring_Maple_01`, `Flooring_Tile_Squares_01`.

<a name="1.1-examples"></a>
#### Examples

##### Character

| Asset Type               | Asset Name   |
| ------------------------ | ------------ |
| Skeletal Mesh            | SK_Bob       |
| Material                 | M_Bob        |
| Texture (Diffuse/Albedo) | T_Bob_D      |
| Texture (Normal)         | T_Bob_N      |
| Texture (Evil Diffuse)   | T_Bob_Evil_D |

##### Prop

| Asset Type               | Asset Name   |
| ------------------------ | ------------ |
| Static Mesh (01)         | SM_Rock_01   |
| Static Mesh (02)         | SM_Rock_02   |
| Static Mesh (03)         | SM_Rock_03   |
| Material                 | M_Rock       |
| Material Instance (Snow) | MI_Rock_Snow |

<a name="asset-name-modifiers"></a>
### 4.2 Asset Name Modifiers

When naming an asset use these tables to determine the prefix and suffix to use with an asset's [Base Asset Name](#base-asset-name).

#### Sections

> 4.2.1 [Most Common](#anc-common)

> 4.2.2 [Animations](#anc-animations)

> 4.2.3 [Artificial Intelligence](#anc-ai)

> 4.2.4 [Prefabs](#anc-prefab)

> 4.2.5 [Materials](#anc-materials)

> 4.2.6 [Textures](#anc-textures)

> 4.2.7 [Miscellaneous](#anc-misc)

> 4.2.8 [Physics](#anc-physics)

> 4.2.9 [Audio](#anc-audio)

> 4.2.10 [User Interface](#anc-ui)

> 4.2.11 [Effects](#anc-effects)

<a name="anc-common"></a>
#### Most Common

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Level / Scene           |  *          |            | [Should be in a folder called Levels.](#levels) e.g. `Levels/A4_C17_Parking_Garage.unity` |
| Level (Persistent)      |            | _P         |                                  |
| Level (Audio)           |            | _Audio     |                                  |
| Level (Lighting)        |            | _Lighting  |                                  |
| Level (Geometry)        |            | _Geo       |                                  |
| Level (Gameplay)        |            | _Gameplay  |                                  |
| Prefab                  |        |            |                                  |
| Material                | M_         |            |                                  |
| Static Mesh             | SM_       |            |                                  |
| Skeletal Mesh           | SK_       |            |                                  |
| Texture                 | T_         | _?         | See [Textures](#anc-textures)    |
| Particle System         | PS_       |            |                                  |

<a name="anc-models"></a>

#### 4.2.1a 3D Models (FBX Files)

PascalCase

| Asset Type    | Prefix | Suffix | Notes |
| ------------- | ------ | ------ | ----- |
| Characters    | CH_    |        |       |
| Vehicles      | VH_    |        |       |
| Weapons       | WP_    |        |       |
| Static Mesh   | SM_    |        |       |
| Skeletal Mesh | SK_    |        |       |
| Skeleton      | SKEL_  |        |       |
| Rig           | RIG_   |        |       |

#### 4.2.1b 3d Models (3ds Max)

All meshes in 3ds Max are lowercase to differentiate them from their FBX export.

| Asset Type    | Prefix | Suffix      | Notes                                   |
| ------------- | ------ | ----------- | --------------------------------------- |
| Mesh          |        | _mesh_lod0* | Only use LOD suffix if model uses LOD's |
| Mesh Collider |        | _collider   |                                         |

<a name="anc-animations"></a>

#### 4.2.2 Animations 
| Asset Type           | Prefix | Suffix | Notes |
| -------------------- | ------ | ------ | ----- |
| Animation Clip       | A_     |        |       |
| Animation Controller | AC_    |        |       |
| Avatar Mask          | AM_    |        |       |
| Morph Target         | MT_    |        |       |

<a name="anc-ai"></a>
#### 4.2.3 Artificial Intelligence

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| AI Controller           | AIC_     |            |                                  |
| Behavior Tree           | BT_      |            |                                  |
| Blackboard              | BB_       |            |                                  |
| Decorator               | BTDecorator_ |          |                                  |
| Service                 | BTService_ |            |                                  |
| Task                    | BTTask_  |            |                                  |
| Environment Query       | EQS_     |            |                                  |
| EnvQueryContext         | EQS_     | Context    |                                  |

<a name="anc-prefab"></a>
#### 4.2.4 Prefabs

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Prefab         |        |            |                                  |
| Prefab Instance         | I       |            |                                  |
| Scriptable Object       |     |        | Assigned "Blueprint" label in Editor |

<a name="anc-materials"></a>

#### 4.2.5 Materials
| Asset Type        | Prefix | Suffix | Notes |
| ----------------- | ------ | ------ | ----- |
| Material          | M_     |        |       |
| Material Instance | MI_    |        |       |
| Physical Material | PM_    |        |       |

<a name="anc-textures"></a>

#### 4.2.6 Textures
| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Texture                 | T_         |            |                                  |
| Texture (Diffuse/Albedo/Base Color)| T_ | _D      |                                  |
| Texture (Normal)        | T_         | _N         |                                  |
| Texture (Roughness)     | T_         | _R         |                                  |
| Texture (Alpha/Opacity) | T_         | _A         |                                  |
| Texture (Ambient Occlusion) | T_     | _AO      |                                  |
| Texture (Bump)          | T_         | _B         |                                  |
| Texture (Emissive)      | T_         | _E         |                                  |
| Texture (Mask)          | T_         | _M         |                                  |
| Texture (Specular)      | T_         | _S         |                                  |
| Texture (Packed)        | T_         | _*         | See notes below about [packing](#anc-textures-packing). |
| Texture Cube            | TC_       |            |                                  |
| Media Texture           | MT_       |            |                                  |
| Render Target           | RT_       |            |                                  |
| Cube Render Target      | RTC_     |            |                                  |
| Texture Light Profile   | TLP_     |            |                                  |

<a name="anc-textures-packing"></a>

#### 4.2.6.1 Texture Packing
It is common practice to pack multiple layers of texture data into one texture. An example of this is packing Emissive, Roughness, Ambient Occlusion together as the Red, Green, and Blue channels of a texture respectively. To determine the suffix, simply stack the given suffix letters from above together, e.g. `_ERO`.

> It is generally acceptable to include an Alpha/Opacity layer in your Diffuse/Albedo's alpha channel and as this is common practice, adding `A` to the `_D` suffix is optional.

Packing 4 channels of data into a texture (RGBA) is not recommended except for an Alpha/Opacity mask in the Diffuse/Albedo's alpha channel as a texture with an alpha channel incurs more overhead than one without.
<a name="anc-misc"></a>

#### 4.2.7 Miscellaneous

| Asset Type                      | Prefix | Suffix | Notes |
| ------------------------------- | ------ | ------ | ----- |
| Universal Render Pipeline Asset | URP_   |        |       |
| Post Process Volume Profile     | PP_    |        |       |
| User Interface                  | UI_    |        |       |

<a name="anc-physics"></a>
#### 4.2.8 Physics

| Asset Type        | Prefix | Suffix | Notes |
| ----------------- | ------ | ------ | ----- |
| Physical Material | PM_    |        |       |

<a name="anc-audio"></a>

#### 4.2.9 Audio

| Asset Type     | Prefix | Suffix | Notes                                                        |
| -------------- | ------ | ------ | ------------------------------------------------------------ |
| Audio Clip     | A_     |        |                                                              |
| Audio Mixer    | MIX_   |        |                                                              |
| Dialogue Voice | DV_    |        |                                                              |
| Audio Class    |        |        | No prefix/suffix. Should be put in a folder called AudioClasses |

<a name="anc-ui"></a>
#### 4.2.10 User Interface
| Asset Type       | Prefix | Suffix | Notes |
| ---------------- | ------ | ------ | ----- |
| Font             | Font_  |        |       |
| Texture (Sprite) | T_     | _GUI   |       |

<a name="anc-effects"></a>
#### 4.2.11 Effects
| Asset Type      | Prefix | Suffix | Notes |
| --------------- | ------ | ------ | ----- |
| Particle System | PS_    |        |       |
**[⬆ Back to Top](#table-of-contents)**

<a name="asset-workflows"></a>

## 5. Asset Workflows

This section describes best practices for creating and importing assets usable in Unity.

<a name="toc"></a>
### Sections

> 5.1 [Unity Asset Import Settings](#unityimport)
>
> 5.2 [3ds Max](#3dsmax)
>
> 5.3 [Textures](#textures)
>
> 5.4 [Audio](#audio)

<a name="unityimport"></a>

### 5.1 Unity Asset Import Settings

Unity's [AssetPostprocessor](https://docs.unity3d.com/ScriptReference/AssetPostprocessor.html) lets you hook into the import pipeline and run scripts prior to or after importing assets. This allows you to enforce import settings when assets are first imported into the project. For example textures that end with `_N` can be marked as a Normal Map on import.

Example guide for Import Settings:

https://github.com/justinwasilenko/Unity-AssetPostProcessor

<a name="3dsmax"></a>
### 5.2 3ds Max

Unity guide on importing from 3ds Max:

https://docs.unity3d.com/2017.4/Documentation/Manual/HOWTO-ImportObjectMax.html

Unity tutorial on the FBX Exporter Package for FBX roundtrip:

https://learn.unity.com/project/3ds-max-to-unity-pipeline

#### Setting up 3ds Max

Unity uses 1 unit = 1 meter. Setup 3ds Max to use Meters by going to ```Customize/Units Setup/System Unit Setup``` and set to 1 Unit = 1 Meter. Using the correct scale is very important for correct Physics / GI / and VR interaction.

Animation frame rate in 3ds Max should be set to 30fps. The ```Time Configuration``` dialog box has 3ds Max's FPS settings

##### Working with Small Objects

* Set ```Customize > Customize User Interface > Mouse Wheel Zoom Increment``` to 0.1m to stop over zooming

* Turn on Viewport Clipping and set the slider on the side of the viewport to be able to zoom in on small meshes. (https://knowledge.autodesk.com/support/3ds-max/learn-explore/caas/sfdcarticles/sfdcarticles/Viewport-Clipping.html)

#### Modeling in 3ds Max

* Follow the [asset naming convention](#anc-models)
* Avoid super long thin triangles (Speeds up tile based renderers & helps with proper GI baking)
* Use Area and Angle Weighted Mesh Normals (Unity Import Setting or Create in 3ds Max)

#### Exporting from 3ds Max into Unity

##### Export Settings:

- Triangulate On
- Tangents and Binormals Off
- Smoothing Groups On
- Preserve edge orientation On
- Units - Automatic Off / Scene Units converted to Meters
- Axis Conversion Z-up

Models created in 3ds Max use a different coordinate system then Unity. Models need to have their pivot point rotated +90 degrees on the X axis to import into Unity correctly.

To do this quickly, open the MaxScript editor, paste this code and select and drag this code on to a Toolbar in 3ds Max to create a button that will run this script. It applies a Xform modifier to rotate the pivot before exporting.

```
fn RotateCreationPivot obj rot =
(
select obj
modPanel.addModToSelection (XForm ()) ui:on
obj.modifiers[#XForm].gizmo.rotation += rot as quat
rotate obj (inverse rot as quat)
)
RotateCreationPivot $ (eulerToQuat(eulerAngles 90 0 0))
```


Script to rotate all objects in 3ds Max scene for export

```
(
    mapped fn ProcessObjectsForUnity node =
    (
        resetxform node
        tm = rotatexmatrix 90
        tm.row4 = node.pos
        node.transform = tm
        node.objectoffsetrot = eulerangles -90 0 0
    )
    
    ProcessObjectsForUnity geometry
)
```

* Batch Exporter for 3ds Max (http://www.strichnet.com/improving-the-fbx-workflow-between-3ds-max-and-unity3d/)

##### Exporting CAT Animation to FBX

Bind normal bones to the CAT rig for use in skinning and exporting

###### Bind Pose

Set Motion Panel/Layer Manager/"Setup/Animation Mode" Toggle to ```Red```
Select only the bones and the mesh you wish to export
Export naming: ModelName.FBX

###### Animation

Set Motion Panel/Layer Manager/"Setup/Animation Mode" to ```Green```
Select ONLY the bones required in your hierarchy (These should match the exact same bones used for Bind Pose), don't include the mesh.
Export naming: ModelName@AnimationName.FBX
The @ symbol is a special Unity naming convention allowing the animation to be bound to the Human.fbx in the Unity editor

#### Importing from 3ds Max into Unity

If importing only animation or bones from a FBX: 

* Set ```Preserve Hierarchy Model``` import option to ```True```
* Set ```Rig > Avatar Definition``` to ```Copy From Other Avatar```

MaxListener Window, set width and height of selected bones, maybe objects too?
$.width = 0.01
$.height = 0.01

**[⬆ Back to Top](#table-of-contents)**

<a name="textures"></a>
### 5.3 Textures

* Textures follow the [naming convention](#anc-textures) found above. 
* They are a power of two (For example, 512 x 512 or 256 x 1024).
* Use Texture Atlases wherever possible.
* 3D software should point to the Unity project textures for consistency when you save or export.
* It is better to resize the texture in Photoshop then to use Unity’s compression options when the in game texture resolution is already known. This reduces the file size and import time of the texture into Unity.
* When working with a high-resolution source PSD outside your Unity project use the same name for both the high-resolution and the imported Unity file. This allows quick iteration when swapping between the 2 textures.

More information for importing textures can be found here: [https://docs.unity3d.com/Manual/ImportingTextures.html](https://docs.unity3d.com/Manual/ImportingTextures.html)

Textures requiring the use of a Alpha channel should follow this guide: [https://docs.unity3d.com/Manual/HOWTO-alphamaps.html](https://docs.unity3d.com/Manual/HOWTO-alphamaps.html)

##### Texture File Format

All textures should be of the .PSD format. No layers should be included and only one Alpha channel in the imported file.

**[⬆ Back to Top](#table-of-contents)**

<a name="audio"></a>
### 5.4 Audio

Only import uncompressed audio files in to Unity using WAV or AIFF formats.

Great guide on [Unity Audio Import Optimization](https://www.gamasutra.com/blogs/ZanderHulme/20190107/333794/Unity_Audio_Import_Optimisation__getting_more_BAM_for_your_RAM.php)

**[⬆ Back to Top](#table-of-contents)**



#### Article References:
https://unity3d.com/learn/tutorials/topics/tips/large-project-organisation
https://github.com/Allar/ue4-style-guide
http://www.arreverie.com/blogs/unity3d-best-practices-folder-structure-source-control/

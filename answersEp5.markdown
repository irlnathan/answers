##Where do I put my css and javascript assets in sails?

Sails uses [grunt](http://gruntjs.com/) to manage assets.  Some of this "management" involves syncing files between your project folder structure and the server's public folder, but as always, I'm getting ahead of myself.

The configuration of `grunt` is based upon the `Gruntfile.js` file found in the root of your sails project.  There’s a lot going on in this file, however, I’m going to concentrate on the javascript and css assets.

### Your Project's Assets
When you first create a project, you have the option of using the `--linker` flag.  An example of using the flag would be `sails new projectName --linker`. Here’s the directory structure of the `/assets` folder under both scenarios:

**USING** the `--linker` flag
``` html
/assets
  /images
  /linker
    /js
    /styles
    /templates
```

**NOT USING** the `--linker` flag
``` html
/assets
  /images
  /js
  /styles
```

Note, you can “upgrade” a project that wasn't created with the `--linker` flag by manually creating the `/linker` folder and inserting it into your `/assets` path.  You can then add `/js`, `/styles`, and `/templates` under `/linker`.

### The Server's Public Folder

When starting the sails server via `sails lift` the following folder structure is created/sync'd via `grunt` within the `.tmp` folder:

``` html
.tmp
  /public
```
  
If any of the other project folders (e.g. `/images`, `/js`, `/styles`, `/templates`) contain content they are copied/sync'd to the `.tmp/public`folder.  The distinction being that if a `/linker` folder exists, the `/js`, `/styles`, and an additional `/templates` folder is created under `/linker`.	

###What happens to my `layout.ejs` file?
If you use the `/linker` folder, sails will alter your `layout.ejs` file to include links to your javascript and css files.  Therefore, any page served from the project's `/views` folder will have access to the javascript and css contained in these files.  

Grunt uses commented tags in `layout.ejs` to as placehodler for these links.  For example, anything placed in the `/style` folder will automatically be linked in `layout.ejs` between these two tags:

``` html
<!--STYLES-->    
<!--STYLES END-->
```

Anything in the `/js` folder will be linked between these two tags:

``` html
<!--SCRIPTS-->
<!--SCRIPTS END-->
```

Anyting in the `/templates` folder will be linked between these two tags:

``` html
<!--TEMPLATES-->   
<!--TEMPLATES END-->
```

### Accessing Sail's Assets
Here's how you access the assets under either scenario: 


**USING** the `/linker` folder

``` HTML
/js --> /linker/js/yourFile.js

/styles --> /linker/styles/yourCSS.css
```

**NOT USING** the `/linker` folder

``` HTML
/js --> /js/yourFile.js

/styles --> /styles/yourCSS.css
``` 
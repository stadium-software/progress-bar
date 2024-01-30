# Vertical Progress Bar

## Description
A sample application that contains a vertical progress bar to show workflow steps in 'done', 'current' or 'todo' states. The sample contains a static implementation as well as one that is generated on page load from data provided in a list. The look and feel is customisable using the variables provided in the *progress-bar-variables.css* file. 

https://github.com/stadium-software/progress-bar/assets/2085324/111b1d76-1987-40e3-b0ee-1548c729423c

## New Module
**Please note**: this module below is being deprecated and will (eventually) be removed altogether. It has been replaced by the [Workflow Steps](https://github.com/stadium-software/workflow-steps) module. 

## Version
1.1 Create a CSS folder in your EmbeddedFiles folder to house the CSS files from this repo

<hr>

## Application Setup
1. Check the *Enable Style Sheet* checkbox in the application properties

<hr>

## Static Progress Bar
Each static progress bar must be created using a set of Stadium controls

### Page Setup
1. Drag a *Flexbox* control to a page and name it "ProgressBarContainer"
2. Add a class called "progress-bar-container" to the "ProgressBarContainer" control *Classes* property 

### Creating a step
Each step added into the "ProgressBarContainer" control needs to end up looking like this<br>
![StadiumDesigner_8seIX8j0xH](https://github.com/stadium-software/progress-bar/assets/2085324/d73af593-e096-4eb0-b2ea-9cec0ba84a12)
<br>You can place as many steps as you need underneath each other

<strong>Static Controls Map</strong>
| | Control | Location | Name | class | Text |
| --- | --- | --- | --- |--- |---
| 1. | Flexbox | page | ProgressBarContainer| progress-bar-container | |
| 2. | Flexbox | ProgressBarContainer | ProgressBarItemContainer| progress-bar-item-container | |
| 3. | Container | ProgressBarItemContainer | ProgressBarStepIcon| progress-bar-step-icon | |
| 4. | Label | ProgressBarStepIcon | ProgressBarStepIconLabel|  | Step description |
| 5. | Label | Next to "ProgressBarStepIcon" | ProgressBarStepLabel| progress-bar-step-label | Step number |

<hr>

## Dynamic Progress Bar
The dynamic version is created from a list of items in a script or event handler using Javascript only. This allows for dynamically generating a progress bar using a dataset from a database or API. 

### Page Setup
1. Drag a *Flexbox* control to a page and name it "ProgressBarContainer"
2. Add a class called "progress-bar-container" to the "ProgressBarContainer" control *Classes* property 

### Type Setup
1. Create a new type in Types in the Application Explorer called "ProgressBarItem"
2. Add two properties to this type. Both properties must be of type *Any*
   1. status
   2. label

### Script Setup
1. Create a script under the page and call it "CreateProgressBarElement"
2. Add two *Input Parameters* to the script
   1. status
   2. label
3. Drag a Javascript action into the script and add the Javascript below into the *Code* property
```javascript
/* Stadium Script Version 1.1 */
let container = document.createElement("div");
container.classList.add("progress-bar-item-container");
container.classList.add(~.Parameters.Input.status);
container.style.display = "flex";
container.style.flexDirection = "row";

let icon = document.createElement("div");
icon.classList.add("progress-bar-step-icon");
let allPBars = document.querySelectorAll(".progress-bar-item-container");
icon.innerHTML = allPBars.length + 1;

let description = document.createElement("div");
description.classList.add("progress-bar-step-label");
description.innerHTML = ~.Parameters.Input.label;

container.appendChild(icon);
container.appendChild(description);

let progressbar = document.querySelector(".progress-bar-container");
progressbar.appendChild(container);
```

### Page.load Setup
1. Drag a List from the Toolbox into the page.load event handler
2. In the *Item Type* property of the list, select "ProgressBarItem" under *Types*
3. Add values to the list *Value* property as required
4. Drag a *ForEach* action below the List and assign the List to the *List* property
5. Drag the *CreateProgressBarElement* script into the *Loop* of the *ForEach* action
    1.  Assign the *ForEach.label* value to the *label* script *Input Parameters* property
    2.  Assign the *ForEach.status* value to the *status* script *Input Parameters* property

<hr>

## StyleSheet CSS
The look and feel of the progress bar can be adjusted using a set of CSS variables located in the attached *progress-bar-variables.css* file. 

1. Open the CSS file called [*progress-bar-variables.css*](progress-bar-variables.css) from this repo in an editor of your choice (I recommend [VS Code](https://code.visualstudio.com/))
2. Adjust the variables in the *:root* element as you see fit

## Applying the CSS
How to apply the CSS to your application

### Stadium 6 (versions 6.6 and above)
1. Create a folder called *CSS* in the EmbeddeFiles folder in your application 
2. Add the two CSS files to that folder
3. Paste the link tags below into the *head* property of your application
```html
<link rel="stylesheet" href="{EmbeddedFiles}/CSS/progress-bar.css">
<link rel="stylesheet" href="{EmbeddedFiles}/CSS/progress-bar-variables.css">
``` 

<hr>

## Upgrading
To upgrade this module
1. Pull the latest repo
2. If you have made changes to the *progress-bar-variables.css* file in your local repo, merge them
3. You can drag the *progress-bar.css* file into the EmbeddedFiles folder of your application as is
4. Select "Overwrite" when prompted in Stadium
5. Open the *progress-bar-variables.css* file 
6. If new variables were added, change the variables as you see fit 
7. Drag the updated *progress-bar-variables.css* file into the EmbeddedFiles folder of your application

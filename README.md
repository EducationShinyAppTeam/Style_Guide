Style Guide
================
Neil Hatfield (<njh5464@psu.edu>), Robert Carey (<rpc5102@psu.edu>)

Last Updated: 21 May 2020

---
This guide spells out the styling that should be used for all apps
included in [BOAST](https://github.com/EducationShinyAppTeam/BOAST). Keep in mind that there are several different aspects to what makes up Style including:

  - Coding (how you write, organize, and comment the code that makes the app)
  - Visual Appearance (how you make the app look including tabs, fonts, colors, icons, etc.)
  - Wording (how you write information, instructions, and other messages to the users)
  - Documentation (how you provide references, including code and data sources, and give credit)

By following this style guide you’ll ensure that any app you create will
meet our standards.

---
## Table of Contents
  - [Getting Started](#getting-started)
    - [Checklist](#checklist)
    - [`boastUtils` Package](#boastutils-package)  
    - [Sample App](#sample-app)
  - [Coding Style](#coding-style)
      - [General Coding Style](#general-coding-style)
      - [Organizing Code](#organizing-code)
      - [Metadata](#metadata)
      - [CSS](#css)
  - [Visual Appearance](#visual-appearance)
      - [PSU Branding](#psu-branding)
      - [Dashboard (Overarching App Structure and Tabs)](#dashboard)
      - [Common Elements (Input Ordering, Buttons, Hover Text, etc.)](#common-elements)
      - [Colors](#colors)
      - [Text Styling](#text-styling)
      - [Graphics](#graphics)
      - [Miscellaneous](#miscellaneous)
  - [Wording](#wording)  
      - [General Guidelines](#general-guidelines)
      - [Popovers](#popovers)
  - [Documentation](#documentation)
      - [References](#references)
      - [Plagiarism](#plagiarism)
      - [`R` Packages](#r-packages)
      - [Graphics](#graphics)
      - [Data](#data)
  - [Accessibility](#accessibility)
  - [Mobile Friendliness](#mobile-friendliness)
  - [Additional Tools](#additional-tools)

---

## Getting Started
Before you get too far into the Style Guide, we would like for you to take a moment and ensure that you have the following tools at your disposal.

### Checklist
1. Ensure that you have all of necessary accounts and if not, put in a request to Robert (Bob).  
    a. DataCamp  
    b. GitHub  
    c. EducationShinyAppTeam on GitHub  
    d. ~~RStudio Server~~  
          + Upon investigation the TLT and the Eberly RStudio Servers will not be useful for us to do testing. An alternate testing process will be explored.  
    e. BOAST in Teams (tied to your PSU ID)
2. Ensure that you have all of the proper software.  
    a. `R` (version 3.5.* minimum, version 4.0.0 preferred)  
    b. RStudio (most current version preferred)  
3. Additional Software that we recommend  
    a. GitHub Desktop  
4. `R` Packages--here are some basic packages that everyone will need; be sure to install their dependencies too  
  a. `tidyverse`  
  b. `ggplot2`  
  c. `shiny`  
  d. `shinyBS`  
  e. `boastUtils` (see below)  
5. A copy of the Sample App (see below)

### `boastUtils` Package
Bob created the [boastUtils](https://github.com/EducationShinyAppTeam/boastUtils) package to automate much of the design and development process. This will not only reduce the amount of work you’ll need to do, it’ll also make apps more consistent. 
 
__Starting Summer 2020, you will be required to you make use of this tool.__

Please check out the package’s
[page](https://github.com/EducationShinyAppTeam/boastUtils) for
instructions on installing and usage.

### Sample App  
Bob and Neil have created a Sample App repository that you can use as a template for your own apps. To get started, clone the
[Sample\_App](https://github.com/EducationShinyAppTeam/Sample_App)
template repo found on GitHub. This will provide you with a skeleton for
organizing your files as well as your code. There are several methods you can use:

#### Command Line
Enter the following in your terminal:

``` bash
git clone git@github.com:EducationShinyAppTeam/Sample_App.git
```

#### Direct Download
You can download the repository directly:

  > <https://github.com/EducationShinyAppTeam/Sample_App/archive/master.zip>

#### GitHub Desktop
If you are using GitHub Desktop and have linked your account that has access to the EducationShinyAppTeam repository, you can do the following from inside GitHub Desktop:  

1. Bring up the Clone Repository Menu (File -> Clone Repository...)  
2. Enter Sample\_App in the search bar and select the option that says Sample\_App (not sampleapp)
3. Click the Choose... button for the local path (this is where you want to the clone to live on your computer)
4. Click the Clone button.

[Back to ToC](#table-of-contents)

---

## Coding Style
Now that you've gone through the Getting Started section, we can turn our attention to the first part of the Style Guide: Coding. There are many aspects that fall under the heading of Coding Style. 

### General Coding Style
Our general practice is to make use of the [tidyverse style guide](https://style.tidyverse.org/). However, we do have some important departures and additional practices you need to follow:

1.  Leave Comments
    
      - At bare minimum, use a comment to break your code into sections.  
          - This helps you and others conceptualize the code into more manageable chunks.  
          - Your comments can provide others with potential keywords to search       for when looking at your code later on.
      - For particularly complex sections, use comments to summarize
        what you’re trying to do.  
        - This can help you and others pick up the coding thread for what you are trying to do for troubleshooting, debugging, and future improvements.

2.  Use Informative Names for Variables and Functions
    
      - Use camelCase for variables and functions. The first word begins with a lowercase letter and additional words start with Capital letters with no space or underscore ( \_ ) between them. (This is a departure from the tidyverse style.)  
      - Use names that give another person a sense of what that variable represents (nouns) or what the function is supposed to do (action verbs). For example,  
          - `scoreMatrix` is a matrix that holds a set of scores  
          - `checkGame` is a function that checks the state of the
            current game  
      - Avoid using the variable names that existed in code you’re making use of from another app or script.  
          - E.g., don’t use `waitTimes` to hold your data on the number of correct answers a user has given.

3.  Format Your Code (see also [Organizing Code](#organizing-code))
    
      - Use indentation spacing to help make your code readable. RStudio has a built-in tool that can help with this.
        
          - Select all of the code you want to reformat. To select all code in a file, use Command-A (Mac) or Control-A (Windows).
          - Press Command-Shift-A (Mac), Control-Shift-A (Windows), or click on the Code menu and select Reformat Code.
          - NOTE: this tool is imperfect and can result in left parenthesis or curly braces moving up a line to where you might have an end-of-line comment, resulting in errors.
    
      - Make use of the `styler` and `lintr` packages to help you perform formatting checks and to quickly reformat code.
    
      - Be Explicit  
          - When passing values to the arguments of a function, be explicit and include the argument name in your code. For example,
        
        ``` r
        actionButton(
          inputId = "submit",
          label = "Submit",
          color = "primary",
          style = "bordered",
          class = "btn-ttt"
        )
        ```  
        - Two exceptions to this would be formula arguments (e.g., `response ~ factor1 + block`) and data vectors/frames (e.g., `dataFrame$response`). These function arguments are generally easy for a person to parse.
        - An additional exception would be functions that stem from the `shiny` and `shinydashboard` packages (e.g., use `dashboardHeader` rather than `shinydashboard::dashboardHeader`). 
    - Remember the following: the more proactive you are from the get go in commenting and organizing your code, the easier time you will have for debugging and improving your code down the road.

4.  Be aware of HTML Tags and how to use them correctly – **Accessibility Issue**
    
    HTML Tags should not be used without some basic understanding of what that tag is for. Using the tags without such an understanding can not only lead to problems with your code running properly or looking like what you intended, but can interfere with how accessible your app is to wider audience. Here are the most common HTML tags that you'll encounter when making a Shiny App.
    
      - List Items – `tags$li()`
          - All list items need to be enclosed in a larger list environment:
              - Use `tags$ol( )` around your items if a user must work through the steps in a particular order. This is the Ordered List environment.
              - Use `tags$ul( )` around your items if a user can jump around the list in any order they wish. This is the Unordered List environment.
          - You do NOT need to use Header or Paragraph tags when you’ve used a list item tag.
          - Exception to List Environment: the Dashboard Header has a built-in listing environment where you do not need to use `tags$ol()` or `tags$ul()`.
      - Heading Tags – `h1()`, `h2()`, `h3()`, `h4()`, `h5()`, and `h6()`:
    
    Heading tags provide a navigational structure to your app. Think of them as being the different levels of titles in a book. They are **NOT** for making text larger, boldface, or other text styling. Think about the headings as laying out a Table of Contents for your app, rather than containing content.
    
      - Hierarchy – there is a specific ordering to the header tags. For
        our apps, this would be:
        
          - `h1()` is for the Title of your App and should be ONCE at the top of the first page that appears when you load the app (i.e., the Overview).
          - `h2()` is for Page titles within the App. These would correspond with the tab links you place in the dashboard’s left side panel.
          - `h3()` is for titling Sections within a Page of the App. These might title the portion of the page that is for a game board, questions, answers, and graphs/plots.
          - `h4()` is for a Subsection within a section. You might use this to distinguish different sets of controls in a Controls section.
          - `h5()` and `h6()` should be used sparingly. These might be used for different levels of a game.
    
      - Avoid skipping heading levels
    
      - DO NOT USE headings to style text (We cannot stress this enough.)
    
      - Do not wrap a header tag around a list element (i.e.,
        `h3(tags$li("here is my list item"))`) nor the reverse (i.e.,
        `tags$li(h3("here is my list item"))`)
    
      - Do not mix header tags together in the same line or with the
        paragraph tag.
    
      - For more information check out the [W3C’s
        Tutorial](https://www.w3.org/WAI/tutorials/page-structure/headings/)
    
      - Paragraph Tag – `p()`: 
    
    Enclose all content text–even if a single sentence–as well as equations in a paragraph environment. This tells screen readers what the content you’ve created and included in your App is. The header tags only create the skeleton while the paragraph tag provides everything else. 

5.  Styling Text  
   
    The styling of text (including font size, font weight (e.g., boldface), font family, color, etc.) is something that we began standardizing in Fall 2019. This is centrally managed by Neil and Bob to ensure 1) consistency across apps, 2) to cut down on the extraneous coding you need to do (this way you can focus on the apps), and 3) ensures that we apps that are accessible and mobile friendly. To this end:
    
      - The styling of text will be controlled using an **external** CSS (Cascading Style Sheet) file. You will implement this depending on what approach you use:
        - If you’re using the `boastApp` function from `boastUtils` (recommended), you don't need to do anything as the appropriate calls will automatically be done for you.  
        - If you are using the `ui.R` and `server.R` format, place the following code in the `tags$head( )` portion at the top of the `dashboardBody` section of your App:
        <!-- end list -->
        ``` r
        tags$link(rel = "stylesheet", type = "text/css", 
        href = "https://educationshinyappteam.github.io/Style_Guide/theme/boast.css")
        ```
    
    There times when you might need some additional text styling that is not already covered. In these cases, __you'll need to talk to Neil or Bob to determine what is the best course of action__. This could entail an addition to the central CSS file or the inclusion of an additional CSS file unique to that app. 
    
    The central CSS file should only be altered by Neil or Bob and covers many aspects. However, this is a living file meaning that we will add to/alter the file as needed to improve the whole set of apps.

6.  Minimize Package Usage
    
      - Make sure that you absolutely have to use a particular package before you do. Check to see if what you’re trying to do can be done in a package you’re already using or in base R.
      - To help you avoid name masking, ensure that you are actually using a package, and to help future readers follow your code, explicitly call packages with their functions.
          - For example, use `dplyr::filter([arguments])` instead of just `filter([argumens])`.
      - Run a `funchir::stale_package_check` on your `app.R`, `ui.R`, and `sever.R` files to see which packages you’re loading might not actualy use.

7.  Minimize External Files
    
    Try to minimize the number and size of external files you’re attaching to your App. If you’re working on an existing App, remove any external files that are no longer necessary.

8.  Plot Caching  
    There are cases when your app will include a plot that falls into any of the following categories:  1) a plot that all users will see (i.e., static data set), 2) is a computationally intense plot (i.e., lots of data and/or layers), 3) might be a dynamic graph that the user explores and needs to move back and forth between various states. Each of these cases represents a place where the performance of your app can suffer. To improve performance, you should consider using the `rednerCachePlot` function rather than `renderPlot`. This function will store a copy of each plot on the sever and provide that stored copy to new instances of the app. This cuts down on server demands and speeds up your app. For the third category, this allows the users to move more quickly to a previously examined state (i.e., low to no hang time).

[Back to ToC](#table-of-contents)

### Organizing Code

There is a fixed order in which you should write your code. This will depend on if you are using a singular `app.R` file or the pair `ui.r` and `server.r`.

#### Using `app.R`

The order for your code will be as follows:

1.  Packages to be loaded
2.  App Metadata (see below)
3.  Any additional source files
4.  UI definition
5.  Server definition
6.  `boastApp` call

#### Using `ui.R` and `server.R`

The order for your code in the `ui.R` file:

1.  Packages to be loaded
2.  App Metadata (see below)
3.  Any additional source files
4.  UI definition

The order for your code in the `server.R` file:

1.  Packages to be loaded
2.  Any additional source files
3.  Server definition

[Back to ToC](#table-of-contents)

### Metadata

Each app will need the following metadata either the `app.R` or the `ui.R` file. For long lines, use the `paste` function to allow you to break code lines apart but end up with a cohesive string for printing. This data is used to teach Learning Management Systems (LMS) and Learning Record Stores (LRS) what your app does. More formats will be supported in the future.

For now, use the following format:

        ```r
        ## App Meta Data----------------------------------------------------------------
        APP_TITLE  <<- "Title of the app"
        APP_DESCP  <<- paste(
            "Description of the app",
            "use multiple lines to keep the description legible.",
        )
        ## End App Meta Data------------------------------------------------------------
        ```

Notice that both `APP_TITLE` and `APP_DESCP` do not follow camelCase. This is by intent to denote global `constants`.

[Back to ToC](#table-of-contents)

### CSS
Cascading Style Sheets (CSS) will be the way to control the visual appearance of all elements of the app. To ensure that we have consistent we will make use of the BOAST CSS throughout. This is relatively new (Winter 2019/Spring 2020), so many of the older apps will need to have this added to their code. This allows us to centralize and dynamically update all apps at once.

There are three key elements at play for CSS:  

1. All apps need to have the appropriate reference to the CSS file (See #5 of [General Coding Style](#genderal-coding-style)).  
    a. Please register any issues, bugs, enhancements, new stylings to the Style Guide repository of GitHub. 
2. Any app specific styling needs to as be in a CSS file and approved
3. There should not be any styling code in the app.R, ui.R, or server.R files (a.k.a. in-line CSS). Styling code would look like this:  
    + `tags$style(HTML(".js-irs-0 .irs-single, .js-irs-0 .irs-bar-edge, .js-irs-0 .irs-bar {background: orange}"))`  
    + `style="color: #fff; background-color: #337ab7; border-color: #2e6da4"`

There is an exception: setting up alignment for a div section: `div(style = "text-align: center"...)` These are allowed in the R files.

If you come across an app that has in-line CSS OR calls to a CSS file that isn't `boast.css`, please log an issue and mention/assign Neil. (Most common external CSS files are `style.css` and `Feature(s).css`.)


[Back to ToC](#table-of-contents)

---
## Visual Appearance
The second portion of this Style Guide deals with the Visual Appearance of each App. Visual Styling encompasses not only text styling but also color scheme usage, graphics (images, plots, tables), and the dashboard layout. For each App, there are 5 major components to the Visual Appearance that you will need to consider: PSU Branding, the Dashboard, Color, Text Styling, and Plots. 

One of the most important benefits of using the `boastApp` function from the `boastUtils` package is that is that much of the Visual Appearance will be automatically handled for you. However, you should still familiarize yourself with the Visual Appearance Style for our apps.

### PSU Branding
Given that we are all associated with Pennsylvania State University, we need to include the Penn State logo in each App. Rather than sticking the logo at the top of the Overview page, we are going to place the logo at the bottom of the sidebar. This has the benefit of having the logo appear throughout the entire App AND making the logo be as unobtrusive as possible.

In your `ui.R` file (or your UI section of `app.R`), at the end of your `dashboardSidebar()` section, include the following:

        ``` r
            tags$div(
              class = "sidebar-logo",
              boastUtils::psu_eberly_logo("reversed")
            )
        ```

This will ensure that the Penn State logo gets properly used.

[Back to ToC](#table-of-contents)

### Dashboard

All Apps will make use of a Dashboard structure. This divides the visual appearance of each App into three main areas. Across the top of the App will be the Header, along the left side of the App will be the navigation list (the Sidebar) where the various Tabs (pages) of your App will be listed. The last area is the Body; this is where all content will appear. 

#### Dashboard Header
The Dashboard Header contains only a couple of elements. The most important of these will be Title of your App. This will automatically be followed by the sidebar collapse/expand button. At the far right, you will then include a link to the home page of BOAST using the Home icon.  

Additional icons might be included to the left of the Home icon. However, these icons remain the same for all Tabs/pages of your App and are thus are not appropriate for Tab specific information.

There should not be any additional elements in the Dashboard Header. Any links for navigate in your App should appear in the Sidebar on the left edge.

#### Sidebar and Body

The Sidebar (responsible for App navigation) and the Body are intimately related to one another. The Sidebar provides structure to the App as well as being the primary way that a user can move around the App. The Body is where all content (text, images, plots, buttons, etc.) exists for the user to read, view, and interact with.

To ensure a consistent experience across all apps, you need to make sure that your App has the following pages and in the following order:

1.  The Overview Tab
      - This Tab is __REQUIRED__ for all Apps. This is the main landing page of your App and should appear at the top of the sidepanel.
      - The icon for this Tab must be "dashboard".
    
      - This Tab must contain __ALL__ of the following elements:
        
        1.  “Title” (as Heading 1)
        2.  A description of the app (as paragraph text under the title)
        3.  “Instructions” (as Heading 2)
        4.  General instructions for using the App (using an Ordered List environment)
        5.  A button that will take the user to the next Tab/page.
        6.  “Acknowledgements” (as Heading 2)
        7.  A listing of acknowledgements including, coders, content writers, etc. (as a paragraph)
        8.  Last Element: `div(class = "updated", "Last Update: mm/dd/yyyy by FL.")` with mm/dd/yyyy replaced with the date of the update you pushed to the server and FL replaced with your initials.
    
      - There is no need to use boldface or colons with the section headings when you properly use Heading tags.
      
2.  A Prerequisites Tab
      - If your App needs to ensure that the user has the base understandings necessary to interact with your App, you’ll need to create a prerequisites Tab. Otherwise, skip this Tab.
      
      - The icon for this Tab must be "book".
      
3.  Activity Tab(s)–At least one is Required
      - This is the heart of your App and is thus required to have at least one.
       
      - In the event you have multiple activities, each one will need a separate Tab. The order of these Tabs will depend upon the your goals for the App.
      
      - Each Tab should contain all information/instructions for the user to be able to interact with the activity without having to switch to other Tabs.
      <!-- end list -->
      - The icon you use depends on the type of activity:
        - Games will use the icon "gamepad".
        - Explorations will use the icon "wpexplorer".
        - Challenges will use the icon "gears".
        
4.  The Last Tab: References–icon: leanpub–REQUIRED
      - This Tab is __REQUIRED__ and is where you will place a reference list for all of the following items that you used in your app:
          - All `R` packages you used
          - Sources of any Code you used directly or drew heavily upon from other people
          - Pictures and/or other images
          - Data sets
      - Refer to the [Documentation Section](#documentation) of this Style Guide for more information.
      
      - The icon for this Tab must be "leanpub".
      
5.  Last Element: Penn State Logo
      - The bottom of the Sidebar should contain the Penn State Logo
        (see the [PSU Branding section](#psu-branding)).

[Back to ToC](#table-of-contents)

#### Tabs Inside the Body
There are two types of tabs in a Shiny app: there are the `tabItem` (i.e., the pages within an app and should appear in the Sidebar) and `tabPanel` (i.e., creating sub-pages or independent sections). In this section, we will discuss this later case.

Deciding on whether to use `tabPanel` is going to depend on several things:

1. Do you have two or more aspects that are related enough that they shouldn't be their own separate tabs/pages of your App?  
    a. If NO, then you shouldn't use `tabPanel`.  
    b. If YES, then continue.
2. Are any of your aspects something that would be better suited as a Challenge or Game tab?  
    a. If YES, move that aspect to a separate page. If you still have 2+ aspects, continue.  
    b. If NO, continue.  
3. Are the aspects independent enough that a person can skip a couple and still use the App successfully?  
    a. If NO, then you should re-consider your design.  
    b. If YES, then proceed with using `tabPanel` in you design.

When you go to make a set of tab panels you will need to first create a `tabsetPanel` which will wrap around all of the individual panels. Use `type = "tabs"`.

The tabs inside the body should automatically appear horizontally and along the top of the tab body (i.e., in the white space below the Dashboard Header). Any visual styling will be managed by the BOAST CSS file at a global level.

[Back to ToC](#table-of-contents)

### Common Elements
In addition to the Dashboard elements of the apps, there are other elements that are common. This include things such as how inputs should be ordered, buttons, and hover text.

#### Ordering Inputs
One of the most powerful aspects of Shiny apps is that the user interacts with them. Thus, we do need to consider not only the ways in which user interact (e.g., buttons, sliders, text entry, etc.) but also the order in which you want the user to manipulate the inputs. Coming up with a single declaration for how to order inputs in all cases is not necessarily feasible. However, we can set up a general guideline for how to make decisions on ordering your inputs.

Please use the following guidelines for determining the order of inputs in the User Interface (UI):

1.  In general, if you want your user to do things in certain order, make your inputs appear in that order.  For example, If you want them to pick a data set, then an unusualness threshold/significance level, what attribute to test, and then set a parameter value, then your inputs should appear in that order.
2. Make use of how we read the English language, i.e., Top-to-Bottom and Left-to-Right to provide an implicit ordering for your user.
3. If a user needs to carry out steps in particular sequence for your App to run properly, then place your inputs inside of an Ordered List environment with explicit text on what they should do. For example,  
    1. Choose your data set: [dropdown]  
    2. Set your unusualness threshold/significance level  
       [slider]  
    3. Which attribute do you want to test: [dropdown]  
    4. What parameter value do you want to use: [numeric input]
4. If an input is going to reset other inputs you should either:  
    a. Warn the user before hand  
    b. Move the input to the top of the list  
    c. Program the input to not reset other inputs  
    d. Some combination of the above  
5. If the inputs are not dynamically linked to the output (e.g., plots automatically update with a change in the input's value), then you should include a button that says "Make Plot" at the end of the inputs.
   
[Back to ToC](#table-of-contents)

#### Buttons
Buttons are one way in which users interact with the apps. The two most common functions that are used are `shiny::actionButton` and `shinyBS::bsButton`. Both functions share many of the same features. Two ways in which they are different is that `shinyBS::bsButton` has an additional `style` argument while `shiny::actionButton` has a `width` argument that gives you fine grain size control.  There are three key styling aspects: shape/animation, color, and text & icon.

##### Shape/Animation
All shape aspects of buttons will be controlled by CSS. The standard shape will be rectangular (the default). Sizing will be controlled by CSS although setting `size = "large"` for the `bsButton` call may be done.

We have a number of apps where a button will change shape/size when a person hovers their cursor over it. This "animation" is to be discontinued. This is to say that buttons which change shape/size should be flagged as issues and resolved at the first opportunity.

At most, the button's color might change (e.g., lighten or darken), depending on the context.

##### Color

The coloring of the button will also be controlled by CSS in one of two ways.

The default way will be through the BOAST CSS. This will ensure that the selected color scheme for your App will be consistent.

The second way only applies to `bsButton` and the `style` argument. Here, this option references an external CSS file beyond BOAST. We see these most often in games. Use the following list to guide you in choosing which style:

+ `warning`: Good for when you want the user to proceed with caution; for example a submit button in a game.
+ `danger`: Good for when you want the user to think twice before clicking; for example, a reset game button.
+ `success`: Good for when you want to convey that the user can proceed safely; for example, a button that advances the user through the game
+ `info`: Good for when you want to give some additional information; for example, a button that triggers game instructions popping up, a button that gives a hint, or a button that might filter a question pool.

When in doubt, use the the `default` style option (or even omit this argument) for `bsButton` or use `actionButton`.

##### Text & Icon
The last styling element of a button is two-fold: the text that is in the button and the icon. 

Here are some guidelines for text of a button:

+ All buttons must have some text. 
+ Generally speaking, the text should be relatively brief and clear. 
  - Don't use "Go to the next page" when you could use "Next"
+ The text should make sense with the action of the button; for example,
  - "Reset" if the button resets something (a game, a plot, inputs)
  - "Submit" if the button triggers the app to grab and process input values
  - "Make Graph" if button causes a graph to be generated
  - "Show/Hide Graph" if a button makes a graph object appear/disappear
  - "Next" if a button moves the user along some path.
+ If the button references something like a particular tab (prerequisites, exploration, etc.), the text should reflect this.
  - "Explore!" for a button that takes a user to an Exploration tab.
  - "Prerequisites" for a button that takes a user to a Prerequisites tab.
  - "Challenge Yourself!" for a button takes a user to a Challenge tab.
  - "Play!" for a button that takes a user to Game tab.
+ If a button references an object like an activity packet or a download prompt the text should refer to that
  - "Activity Packet" for a button that would open up and/or download a packet for the user
  - "Download Data" for a button that would download a data file.
+ Clarity is essential. If there are multiple buttons on the page, make sure that you use clear text for what button does and/or references.

Here are guidelines for the inclusion of icons in a button:

+ Game buttons will NOT have any icons.
+ "Next" buttons will NOT have any icons.
+ A "Prerequisites" button will use the "book" icon
+ All other tab buttons (labels ending with "!") will use the "bolt" icon.
+ A download button will use the "cloud-download" icon.

[Back to ToC](#table-of-contents)

### Colors

Your App needs to have a consistent color scheme throughout. The color scheme should be checked against colorblindness to meet [WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/) Level AA. You can do so at the [Coloring for Colorblindness](https://davidmathlogic.com/colorblind/#%23000000-%23E69F00-%2356B4E9-%23009E73-%23F0E442-%230072B2-%23D55E00-%23CC79A7) website.

There are two major places where coloring comes into play: plots from `R` and the user interface.

#### Color and Plots in `R`

In `R` you can set color theme which you use in `ggplot2`. Here are two custom color palettes that you can use in your App. Additionally, the package `viridis` provides several additional color palettes which are improvements from the the default.

      ``` r
      # boastPalette is based on the Wong color blind set found at the above website.
      boastPalette <- c("#0072B2","#D55E00","#009E73","#ce77a8","#000000","#E69F00","#999999","#56B4E9","#CC79A7")

      # psuPalette is based on Penn State's three official color palettes and checked at the above webite.
      psuPalette <- c("#1E407C","#BC204B","#3EA39E","#E98300","#999999","#AC8DCE","#F2665E","#99CC00")

      # Both palettes get used in the order of what is listed.
      ```
To use these palettes (or ones from `viridis`) with a `ggplot2` object, you'll need to doe the following

      ``` r
      # You will need to first add whichever palette line from above to your code
      boastPalette <- c("#0072B2","#D55E00","#009E73","#ce77a8","#000000","#E69F00","#999999","#56B4E9","#CC79A7")
      
      # Create ggplot2 object
      g1 <- ggplot2::ggplot(data = df, aes(x = x, y = y, color = grp, fill = grp))
      
      # Add your layers
      g1 + ggplot2::geom_points()
      
      # Tell R to use your chosen palette
      g1 + ggplot2::scale_color_manual(values=boastPalette)  # If you use "color" in aes
      g1 + ggplot2::scale_fill_manual(values=boastPalette)  # If you use "fill" in aes
      ```
If you have more groups than eight/nine colors listed in two palettes, consider reworking your examples as you could overwhelm the user with too many colors. (This also applies to using different shapes to plot points.)

#### Color in the User Interface

All aspects of color in the User Interface should be controlled through the CSS file(s). This includes all of the following:

  - Dashboard coloring (Header, Sidepanel, Body)
  - Text coloring
  - Coloring of Controls (including buttons, sliders, and other input fields)

By using CSS, especially through `boastApp`, you’ll be able to ensure that there is consistent coloring throughout your App.

[Back to ToC](#table-of-contents)

### Text Styling

Text styling refers the non-content aspects of the text on the page. This means things such as the use of italics, boldface, alignment, as well as font size and color.

You should let the centralized CSS file do the heavy lifting for text styling. (Again, using `boastApp` will help you.) However, for this to work properly, you will need to tag content appropriately. (See [Coding Style](#coding-style))

If you run into a situation where something element needs styling, __talk to Neil or Bob for help__. You might have come across an element that needs to get added the central CSS file or a bug.

#### Headings

Use the Heading Tags for the short fragments that define the structure of your App. If you find yourself enclosing a complete sentence in Heading tag, you ARE NOT using headings correctly. Notice how the headings in this Style Guide aren’t complete sentences; your App should mimic this. Full sentences appear as regular paragraph text (i.e., enclosed in `p()`) and not be a Heading.

#### Paragraph Text

If you enclose text that gives instructions or other information to your App’s users in `p()` or `li()` (the later should be wrapped in either `tags$ol()` or `tags$ul()`), your App will understand how to style that text correctly. The central CSS file contains controls that set the base font size much larger than Shiny does natively as well as making text sizing dynamic. (This is important for making our apps mobile device friendly.) Again, using `boastApp` makes this process easier.

If you want to make a certain word or phrase italic, you will need to wrap that text in `tags$em()`. Similarly, if you want do the same with boldface, you’ll use `tags$strong()`.

For example, this code:

      ```r
      p(
        "When dealing with the ",
        tags$em("t"),
        "-distribution, we only have one parameter, the ",
        tags$strong("degrees of freedom"),
        "that we need to input."
        )
      ```

Becomes:  

> When dealing with the *t*-distribution, we only have one parameter, the **degrees of freedom** that we need to input.

Use italics (emphasis), and boldface (strong) sparingly.

#### Mathematics

For the most part, any mathematics you need displayed should be done using [MathJax](https://www.mathjax.org/). Default to using inline typesetting with the `\\(` and `\\)` delimiters. If you need to use display style, you can use `\\[` and `\\]`. For the vast majority of mathematics, you’ll wrap both inline and display style mathematics inside of a paragraph environment (`p()`).

If you’re writing mathematics directly in your app, remember you’ll need to escape the LaTeX commands by putting an extra backslash (\\) in front; e.g., `\frac{3}{4}` would need to be `\\frac{3}{4}`.

If you’re reading in mathematical text from an external CSV file, you do not need the extra backslash in the CSV file.

__Note:__ Double dollar sign delimiters are generally not recommended for displaying math as they can lead to unintended results. See: [Writing Mathematics for MathJax](https://docs.mathjax.org/en/latest/basic/mathematics.html).

#### \[Game\] Question Text

The text used as a question in a game should NOT be wrapped in a Heading tag; wrap the text in a paragraph tag.

#### Label Text (Buttons, Sliders, Other Inputs and Alerts)

By using the central CSS file, any text you included in/on buttons, dropdown menus, sliders, radio buttons, choices, and other inputs as well as alert messages and popups/rollovers, will automatically be styled correctly.

Do not use heading tags, the paragraph tag, italics/emphasis, or boldface/strong with input labels.

You may use these tags with popups/rollovers.

#### Feedback and Hint Text

Again, let the central CSS file handle the styling of this type of text.

#### Text in `R` Plots

Unfortunately, any text in `R` plots does not get controlled by CSS. This means that you’ll have to play around with the settings. Using the `ggplot2` package to make your plots (or other packages based upon the ggplot framework) will allow you to use the `theme` aspect to control text in your App.

Here is an example for how to do this:

      ``` r
      # Create a ggplot2 object
      g1 <- ggplot2::ggplot(data=df, aes(x=x, y=y, color=grp)) 
      
      # Add your layers, for example
      g1 + ggplot2::geom_point()
      
      # Use theme to control text size
      g1 + ggplot2::theme(
        plot.caption = element_text(size = 18),
        text = element_text(size = 18)
      )
      ```

You will need to play around with the settings to find the appropriate value; text size 18 does appear to work out well in many cases.

__Note:__ The text in your plot might not behave well for dynamic resizing on different mobile devices.

[Back to ToC](#table-of-contents)

### Graphics
One of the most powerful tools we have in Statistics and Data Science is graphics. This includes images/pictures, graphs/plots, and tables. You will want to make sure that all graphical elements are appropriately sized in the Body. If there is text in a static image/picture, you'll need to make sure that the text is legible on a variety of screen sizes.

We've already discussed both issues of color and text size in plots. For additional considerations, please refer to the following readings (ordered from most important to least):  

  - [Tufte-Fundamental Principles of Analytical Design](https://www.dropbox.com/s/hb52991v09p8q91/Tufte%20-%202006%20-%20The%20Fundamental%20principles%20of%20analytical%20design.pdf?dl=0)
  - [Tufte-Chartjunk](https://www.dropbox.com/s/z8yrf4eqph6c2h4/Tufte%20-%202001%20-%20Chartjunk%20Vibrations%2C%20grids%2C%20and%20ducks.pdf?dl=0)  
  - [Kosslyn-Looking with the Eye and Mind](https://www.dropbox.com/s/62uegsribwdjtze/Kosslyn%20-%202006%20-%20Looking%20with%20the%20eye%20and%20mind.pdf?dl=0)

Remember, we always want to be modeling excellent graphing behaviors.

> All photographs can be fortified with words. --Dorothea Lange

> A picture is worth a thousand words...but which ones. --Unknown

Both of these quotations highlight that you need to include some text with your plots to help the user construct their understanding of what you're trying to show them.


#### Axes and Scales
`R`'s default axes are terrible. They often do not fully cover the data and the have gaps between the axes. All this impedes the user's construction of meaning. Thus, you'll want to take control and stipulate the axes and scales to optimize what users get out of the plot. If you are providing multiple plots that the user is supposed to compare, make sure that they all use the same scaling and axes.

To force `ggplot2` to place (0, 0) in the lower-left corner and to control the scales, you will need to include the following:

      ``` r
      # Create the ggplot2 object
      g1 <- ggplot2::ggplot(...)
    
      # Add your layer
      g1 + ggplot2::geom_point()
    
      # Control axes and scale
      ## Multplicative Scaling of the Horizontal Axis
      g1 + ggplot2::scale_x_continuous(expand = expansion(mult = c(1,2), add = 0)) +
      ## Additive Scaling of the Vertical Axis
      scale_y_continuous(expand = expansion(mult = 0, add = c(0,0.05))) 
      ```
#### Tables
Use tables as infrequently as possible. If you absolutely must include a table, you will need to decide what the role of your table is. This is an Accessibility issue that you __MUST__ pre-plan for. Screen readers will poorly communicate tables if you fail to set the role appropriately. __Talk to Neil and Bob__ before using a table. 

#### Alt Text-Accessibility 
Any graphical element you include in your App __MUST__ have an alternative (assistive) text description ("alt text"). This provides a short description of what is in the image or plot for users who are visual impaired. (Tables, when properly formated will handle this automatically.)

[Back to ToC](#table-of-contents)

### Miscellaneous

Consider adding a loading bar to show the process for intense computations; this will help the user understand that your App is processing and not frozen/broken.

[Back to ToC](#table-of-contents)

---
## Wording

### General Guidelines

When writing the content for your App, you will want to keep in mind that these app have the primary audience of students. Thus, we need to make sure that we use language that is appropriate. Seek to use complete sentences that convey what you intend. Have someone else take a look at your content and then tell you what they believe the text to be saying. If what they say is consistent with what you intended, great. If not, then you need to revise your text.

__DO NOT sacrifice clarity and precision/accuracy for
conciseness/brevity.__

Since these apps are for *teaching*, we need to use language that is accurate and supports students in constructing productive meanings. This means that we need to avoid sloppy language, re-enforcing problematic conceptions, and supporting fallacies. For example,

  - Discussing values of statistics
      - BAD: “The mean is 6.”
      - GOOD: “The value of the *sample arithematic mean* for this data
        is 6 units/object.”
  - Problematic conceptions
      - BAD: “Probability is the likelihood of an event in relation to
        all possible events.”
      - GOOD: “Probability is the long-run relative frequency for us
        seeing a particular data event given our assumptions. Likelihood
        is the long-run relative frequency of a set of assumptions being
        true given our collected data.”
  - Fallacies
     - BAD: "We're 95% confident that the true population proportion is between 0.35 and 0.45."
     - GOOD: "If we were to repeat the entire study infinitely many times, then 95% of the time we will make an interval that captures the true population proportion."

[Back to ToC](#table-of-contents)

### Popovers
Popovers refers to any number of different tools on websites that go by other names such as tooltips, rollovers, and hover text. In essence, this tool appears when the user places their cursor over (i.e., hover) or shifts the focus to a trigger object. The text then pops up on the screen for the user to view. The function to create one of these in a Shiny app is `shinyBS::bsPopover`. While these can be powerful, they are often misused which leads to problems. For example, they can prevent the user from actually interacting with portions of your app when they appear. 

Popovers are meant to provide short, simple clarifications; quick annotations which enrich the content that is already present. This type of text is meant to be temporary, only appearing for as long as the user is hovering/focusing on the trigger object. Thus, if you are putting information that is critical to your user successfully using your App in a popover, you are using popovers __INCORRECTLY__.

Here are few additional sources for reading about Popovers/Tooltips:

+ [Tooltips in UI Design](https://uxplanet.org/tooltips-in-ui-design-f63e117aa3d1)
+ [Tooltips: How to use this small but mighty UI pattern correctly](https://www.appcues.com/blog/tooltips)

Restrict any usage of a popover to something short and non-vital for your App's user. If you do choose to use a popover, you will need to format the popover correctly. Be sure that your function call includes values for the following arguments:

+ `id`: this needs to be the name of the object which will act as the trigger
+ `title`: this will be a string that appears across the top of your popover; use verbs with an understood "you" (e.g., "Investigate!", "Remember", etc.)
+ `content`: this will be the string that you want displayed; shorter is better.
+ `placement`: this will control where the popover appears. Choose the option (top, bottom, left, right) that works best for your space. Ensure that the placement does not cover any controls or other vital information.

[Back to ToC](#table-of-contents)

---
## Documentation

These apps are the product of your hardwork and are part of your academic record. Thus, you need to adhere to [Penn State’s Academic Integrity Policy](https://undergrad.psu.edu/aappm/G-9-academic-integrity.html). This is especially important as we are making the apps available through a Creative Commons Attribution-ShareAlike 4.0 International license ([CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)). If you have used code, pictures, data, or other materials from outside of the BOAST team, you __MUST__ give proper credit. These references will then be included on the App’s References Tab.

### References

All apps will need a References Tab. This is where you’ll place all references for your App, including R packages, borrowed code, data sources, images, etc. This in addition to the Acknowledgements. (NOTE: listing something in the Acknowledgements DOES NOT waive this requirement.)

You may use any citation style you wish, but be consistent. Recommended citation styles include APA and AmStat. Here is a starting code block for you to use:

      ``` r
      tabItem(
        tabName = "refs",
        withMathJax(),
        h2("References"),
        p(class = "hangingindent",
          "reference 1-alphabetically"),
        p(class = "hangingindent",
          "reference 2-alphabetically"),
        # Repeat as needed
      )
      ```

If you need assistance with this section, please talk to Neil.

### Plagiarism

__You MAY NOT use blocks of code you’ve found online without giving
proper attribution.__

There is a difference between looking at example code online to see how to do something and copying that code directly. The former is permissible, the later is plagiarism.  
- If you want to use someone else’s code “as is” (without any changes), you should reach out to the author for permission first. 
- If you use someone else’s code and make modifications, you need to give credit to where you got the code, and potentially ask for permission.

You will need to place citations in *__two__* places: in the References Tab and in your code.

#### Reference Tab Page

Use the following format:

> Author. (Date). Title of program/source code (Version number, if applicable). \[type of code\]. Retrieved from \< URL \>.

For example,

> Hatfield, N. J. (2017). First day activity (v1). \[Netlogo\]. Retrieved from <https://neilhatfield.github.io/statApps/Day1Activity.html>.

#### In Code

Use the following format in your code to cite where you got the code from.

      ``` r
      #-------------------------------------------------------------------------------
      #    Title: <title of program/source code>
      #    Author: <author(s) names>
      #    Date: <date>
      #    Code version: <code version>
      #    Availability: <where it's located>
      #-------------------------------------------------------------------------------
      # [borrowed code then follows]
      # ...
      # [last line of borrowed code]      
      #End of <author>'s code-------------------------------------------------------------------
      ```

[Back to ToC](#table-of-contents)

### `R` Packages

If you made use of any packages in `R`, then you will need to add these to the Reference subsection. Fortunately, there is a built-in tool that will help you: the `citation` function. In R (RStudio) simply type `citation("packageName")` and you’ll get the appropriate citation information for the package you used. For example, `citation("shinydashboard")` and `citation("plyr")` will give the information needed for the following citations:

> Chang, W. and Borges Ribeio, B. (2018). shinydashboard: Create dashboards with ‘Shiny’. (v0.7.1) \[R Package\]. Available from <https://CRAN.R-project.org/package=shinydashboard>

> Wickham, H. (2011). The Split-apply-combine strategy for data analysis. Journal of Statistical Software, 40(1). pp. 1-29. Available at <http://www.jstatsoft.org/v40/i01/>.

Notice, that the format of the R package will depend on whether there is an article published for the package. The `shinydashboard` package is not associated with an article while the `plyr` package is associated with Wickham’s article.

[Back to ToC](#table-of-contents)

### Graphics

Pictures, drawings, photographs, images, etc. are typically copyrighted. When you’re selecting images, make sure that the images are Open Source/Copyright Free/Royalty Free/Public Domain. Additionally, include a reference to where the pictures came from in the Overview Page. The basic format to use is:

> LastName, First Initial. (Year). Title of artwork. \[Format\]. Retrieved from \< URL \>.

[Back to ToC](#table-of-contents)

### Data

If you are using any data files, you need to attribute where those files are coming from in the References subsection of your Overview page. A suggested format to use is:

>Author/Rightsholder. (Year). Title of data set (Version number) \[Description of form\]. Location: Name of producer.  

> Author/Rightsholder. (Year). Title of data set (Version number) \[Description of form\]. Retrieved from <http://www.url.com>

If you (or someone else) had to sign some type of agreement to access the data, we must examine the agreement before you make your App publicly accessible. Just because you got access to the data does not mean you have the right to share the data.

[Back to ToC](#table-of-contents)

---
## Accessibility

We need to make sure that our Apps are accessible. If you have been adhering to the style guide, your App should be in a decent position. When you’re ready to test the accessibility of your App, you’ll need to deploy the App to a sever and then use the [WAVE Web Accessibility Evaluation Tool](https://wave.webaim.org/). Enter the URL of your App in the noted box to run an evaluation. See what accessibility issues your App has and then address them.

__See also:__

  - [Accessibility and Usability at Penn
    State](https://accessibility.psu.edu/)
  - [Accessibility
    Statement](https://www.psu.edu/accessibilitystatement)
  - [How to Meet Web Content Accessibility
    Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
  - [7 Things Every Designer Needs to Know about Accessibility](https://medium.com/salesforce-ux/7-things-every-designer-needs-to-know-about-accessibility-64f105f0881b)

[Back to ToC](#table-of-contents)

---
## Mobile Friendliness

We want our apps to work well with mobile devices. Thus, when you get to the point where the majority of bugs have been fixed, you need to check how mobile friendly your App is. If you have used `boastApp` and/or the `boast.CSS` file, along with the practices laid out earlier, then you should be well on your way to being mobile friendly.

You can check your App in two ways:

1.  Test your App out on a variety of mobile devices.
2.  Make use of a browser’s ability to mimic devices. To do this, launch your App in a browser, then enable one of the following:
      - [Chrome: Device Mode](https://developers.google.com/web/tools/chrome-devtools/device-mode/#viewport)
      - [Firefox: Responsive Design Mode](https://developer.mozilla.org/en-US/docs/Tools/Responsive_Design_Mode)
      - [Microsoft Edge: Device Emulation](https://docs.microsoft.com/en-us/microsoft-edge/devtools-guide/emulation)
      - [Safari: Responsive Design Mode](https://support.apple.com/en-gb/guide/safari-developer/dev84bd42758/mac)

Look for any issues that you might be able to address before you hand off your App for others to play around with. Assign a __Mobile Friendliness Rating__ to your App on a scale from 1 to 5.

1.  Not functional
2.  Functional – Very awkward
3.  Functional – Okay if no big screen available (multiple issues)
4.  Usable in a small class setting (single issue)
5.  Readily usable

[Back to ToC](#table-of-contents)

---
## Additional Tools

Here are a few additional tools that can help you with App development.

  - [lintr](https://github.com/jimhester/lintr) - Checks adherence to a
    given style, syntax errors, and possible semantic issues.
  - [styler](https://www.tidyverse.org/articles/2017/12/styler-1.0.0/) -
    Format R code according to a style guide.
  - [funchir](https://github.com/MichaelChirico/funchir) - stale package
    check

[Back to ToC](#table-of-contents)
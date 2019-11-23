# Style Guide

This guide spells out the styling that should be used for all apps included in BOAST. Styling refers to several different aspects including:
- How you approaching writing code
- Visual appearance of the app
- The wording used in the app
- Documentation of references, including code and data sources

By following this style guide you'll ensure that any app you create will meet our standards.

## boastUtils Package
By using the [boastUtils](https://github.com/EducationShinyAppTeam/boastUtils), you'll be able to automate much of the visual appearance styling. This will reduce the amount of work you'll need to do and worry about. We **strongly** recommend that you make use of this tool.

Please check out the package's [page](https://github.com/EducationShinyAppTeam/boastUtils) for instructions on installing and using this toolkit.

## Writing Code
You should adhere to the [tidyverse style guide](https://style.tidyverse.org/). However, here are some practices you need to follow.

1. Leave Comments
   1. At bare minimum, use a comment to break your code into sections. These can also provide others with potential keywords to search for when looking at your code later on.
   2. For particularly complex sections, use comments to summarize what you're trying to do.
2. Use informative names for variables and functions 
   1. Use names that give another person a sense of what that variable represents or what the function is supposed to do
      + `scoreMatrix` is a matrix that holds a set of scores 
      + `checkGame()` is a function that checks the state of the current game
   2. Avoid using the variable names that existed in code you're making use of from another app or script. 
      + Don't use `waitTimes` to hold your data on the number of correct answers a user has given.
3. Format your code
   1. Use indentation spacing to help make your code readable. RStudio has a built-in tool that can help with this.
      + Select all of the code you want to reformat.  To select all code in a file, use Command-A (Mac) or Control-A (Windows).
      + Press Command-Shift-A (Mac), Control-Shift-A (Windows), or click on the Code menu and select Reformat Code.
      + NOTE: this tool is imperfect and can result in left parenthesis or curly braces moving up a line to where you might have an end-of-line comment, resulting in errors.
   2. Make use of the `styler` and `lintr` packages to help you perform formatting checks and to quickly reformat code.
   3. Be Explicit  
   When passing values to parameters in a function, be explicit and include the parameter name in your code. For example,
      ```r
      actionButton(
        inputId = "submit",
        label = "Submit",
        color = "primary",
        style = "bordered",
        class = "btn-ttt"
      )
     ```
4. Be aware of HTML Tags and use them correctly-- __Accessibility Issue__  
   HTML Tags should not be used without some basic understanding of what that tag is for. Using the tags without such an understanding can not only lead to problems with your code running properly or looking like what you intended, but can interfere with how accessible your app is to wider audience.
   1. List Items--`tags$li()`
      + All list items need to be enclosed in a larger list environment:
         - Use `tags$ol( )` around your items if a user must work through the steps in a particular order. This is the Ordered List environment.
         - Use `tags$ul( )` around your items if a user can jump around the list in any order they wish. This is the Unordered List environment.
      + You do NOT need to use Header or Paragraph tags when you've used a list item tag.
      + Except to Environment:  the Dashboard Header has a built-in listing environment where you do not need to use `tags$ol()` or `tags$ul()`.
    2. Heading Tags--`h1()`, `h2()`, `h3()`, `h4()`, `h5()`, and `h6()`  
        Heading tags provide a navigational structure to your app. Think of them as being the different levels of titles in a book. They are __NOT__ for making text larger, boldface, or other text styling. Think about the headings as laying out a Table of Contents for your app, rather than containing content.
        + Hierarchy--there is a specific ordering to the header tags. For our apps, this would be
           1. `h1()` is for the Title of your App and should be ONCE at the top of the first page that appears when you load the app.
           2. `h2()` is for Page titles within the App. These would correspond with the tab links you place in the dashboard's left side panel.
           3. `h3()` is for titling Sections within a Page of the App. These might title the portion of the page that is for a game board, questions, answers, and graphs/plots.
           4. `h4()` is for a Subsection within a section. You might use this to distinguish different sets of controls in a Controls section.
           5. `h5()` and `h6()` should be used sparingly. These might be used for different levels of a game.
        + Avoid skipping heading levels
        + DO NOT USE headings to style text
        + Do not wrap a header tag around a list element (i.e., `h3(tags$li("here is my list item"))`) nor the reverse (i.e., `tags$li(h3("here is my list item"))`)
        + Do not mix header tags together in the same line or with the paragraph tag.
        + For more information check out the [W3C's Tutorial](https://www.w3.org/WAI/tutorials/page-structure/headings/)
    3. Paragraph Tag--`p()`  
    Enclose all content text--even if a single sentence--as well as equations in a paragraph environment. This tells screen readers what the content you've created and included in your app is. The paragraph tag is what actually gives the structure you defined with header tags a body.
5. Styling Text
   1. The styling of text (including font size, weight, type, colors, etc.) is to be controlled using an __external__ CSS (Cascading Style Sheet).
      + If you are using the `ui.R` and `server.R` format, place the following code inside the `tags$head( )` portion of the dashboardBody:
         ```r
         tags$link(rel = "stylesheet", type = "text/css", 
         href = "https://educationshinyappteam.github.io/Style_Guide/theme/boast.css")
         ```
       + If you're using the `boastApp` function from `boastUtils`, you do not need to worry about this.
   2. If you need to add additional styling that is *unique* to this one app, then you will need to create a specific CCS file for the app and include that file in the app's `www` folder. You'll need to include an instance of the above code, changing the href to `"/[appName].CSS"`.
   3. If you need additional styling that will impact multiple apps, you need to speak with Neil or Bob to see about adding to the main CSS file.
6. Minimize Package Usage
   1. Make sure that you absolutely have to use a particular package before you do. Check to see if what you're trying to do can be done in a package you're already using or in base R.
   2. To help you avoid name masking, ensure that you are actually use a package, and to help future readers follow your code, explicitly call packages with their functions.
       + For example, use `dplyr::filter([arguments])`
    3. Run a `funchir::stale_package_check` on your `app.R`, `ui.R`, and `sever.R` files to see which packages you're loading might not actualy use.
7. Minimize External Files  
   Try to minimize the number and size of external files you're attaching to your app. If you're working on an existing app, remove any external files that are no longer necessary.
8. (*Under development*) Consider using `renderCachePlot` instead of `renderPlot`

## Visual Appearance
The visual appearance of each app consists of 6 major areas (plus one catchall). The benefit of using the `boastApp` function from the `boastUtils` package is that this will automatically take care of much of this section for you.

### Coloring
The app needs to have a consistent color scheme throughout. The color scheme should be checked against colorblindness. You can do so at the [Coloring for Colorblindness](https://davidmathlogic.com/colorblind/#%23000000-%23E69F00-%2356B4E9-%23009E73-%23F0E442-%230072B2-%23D55E00-%23CC79A7) website.

There are two major places where coloring controls come into play: plots from `R` and the user interface.

#### Plots in `R`
In `R` you can set color theme which you would then use in conjunction with `ggplot2`:
```r
# boastPalette is based on the Wong color blind set found at the above website.
boastPalette <- c("#0072B2","#D55E00","#009E73","#ce77a8","#000000","#E69F00","#999999","#56B4E9","#CC79A7")
# psuPalette is based on Penn State's three official color palettes and checked at the above webite.
psuPalette <- c("#1E407C","#BC204B","#3EA39E","#E98300","#999999","#AC8DCE","#F2665E","#99CC00")

# Both palettes get used in the order of what is listed.

g1 <- ggplot2::ggplot(data=df, aes(x=x, y=y, color=grp)) #create a ggplot object

g1 + scale_color_manual(values=boastPalette)  # If you use "color" in aes
g1 + scale_fill_manual(values=boastPalette)  # If you use "fill" in aes
```
#### User Interface
All aspects of color in the User Interface should be controlled through the CSS file(s). This includes all of the following:
   + Dashboard coloring (header, sidepanel, main page)
   + Text coloring
   + Coloring of Controls (including, buttons, sliders, and other input fields)
   
By using CSS, especially through `boastApp`, you'll be able to ensure that there is consistent coloring throughout your app.

### Text Styling
Text styling refers the non-content aspects of the text on the page. This means things such as the use of italics, boldface, alignment, as well as font size and color. 

You should let the `boast.CSS` file do the heavy lifting setting up the styling. (Again, using `boastApp` will help you.) However, you will need to tag content appropriately

#### Headings
Use the Heading Tags for the short fragments that define the structure of your app. If you find yourself enclosing a complete sentence in Heading tag, you ARE NOT using headings correctly. Notice how the headings in this Style Guide aren't complete sentences; mimic this in your app. Full sentences appear as regular paragraph text (i.e., enclosed in `p()`).

#### Paragraph Text
If you enclose text that gives instructions or other information to your app's users in `p()` or `li()`, your app will understand how to style that text correctly.  The `boast.CSS` file contains controls that set the base font size much larger than shiny does natively.  Again, using `boastApp` makes this process easier.

If you want to make a certain word or phrase italic, you will need to wrap that text in `tags$em()`. Similarly, if you want do the same with boldface, you'll use `tags$strong()`. For example, this code
```r
p(
  "When dealing with the ",
  tags$em("t"),
  "-distribution, we only have one parameter, the "
  tags$strong("degrees of freedom"),
  "that we need to input."
)
``` 
turns into --> When dealing with the *t*-distribution, we only have one parameter, the **degrees of freedom** that we need to input.

Use italics/emphasis, and boldface/strong sparingly.

#### Mathematics
For the most part, any mathematics you need displayed should be done using MathJax. Default to using inline typesetting with the `\\(` and `\\)` delimiters. If you need to use display, you can use `\\[` and `\\]` or double dollars signs. For the vast majority of mathematics, you'll wrap both inside of the paragraph environment. 

If you're writing mathematics directly in your app, remember you'll need to escape the LaTeX commands by putting an extra \ in front; e.g., `\frac{3}{4}` would need to be `\\frac{3}{4}`.

If you're reading in text from an external CSV file, you do not need the extra backslash.

#### [Game] Question Text
The text used as a question in a game should NOT be wrapped in a Heading tag; they should be either wrapped in a standard paragraph tag.

#### Label Text (Buttons, Sliders, Other Inputs and Alerts)
If you are using the `boast.CSS` file, the text that is included in/on buttons, dropdown menus, sliders, radio buttons, choices, and other inputs as well as alert messages and popups/rollovers, will automatically be styled corrected. 

Do not use heading tags, the paragraph tag, italics/emphasis, or boldface/strong with input labels; you may use these tags with popups/rollovers.

#### Feedback and Hint Text
Again, let the `boast.CSS` file handle the styling of this type of text.

#### Text in `R` Plots
Unfortunately, text in `R` plots do not get controlled by CSS at this time. This does mean that you'll have to play around with the settings.  Using the ``ggplot2` package to make your plots (or other packages based upon the ggplot framework) will allow you to use the `theme` aspect to control text in your app. Here is an example for how to do this:
```r
g1 <- ggplot2::ggplot(data=df, aes(x=x, y=y, color=grp)) #create a ggplot object

g1 + theme(
  plot.caption = element_text(size = 18),
  text = element_text(size = 18)
  )
```
You will need to play around with the settings to find the appropriate value; 18 does appear to work out well.

### Tab Page Ordering in the Dashboard's Sidepanel
The ordering of the Tab Pages for your App should make logical sense and should structure how you want users to use your App. Additionally, we have specific icons that should be used with particular Tab Pages.

1. Overview--icon: dashboard--REQUIRED
   + This tab page is required for all Apps. This is the main landing page of your app and should appear at the top of the sidepanel.
   + Will contain the following elements
      1. "Title" (as Heading 1)
      2. A description of the app (as paragraph text under the title)
      3. "Instructions" (as Heading 2)
      4. A list of instructions (using an Ordered List environment)
      5. A button that will take the user to the next page.
      6. "Acknowledgements" (as Heading 2)
      7. A listing of acknowledgements including, coders, content writers, etc. (as a paragraph)
      8. "References" (as Heading 3)
      9. A listing of any external sources of code, pictures, or data used in your app that you did not create (as a paragraph)
      10. Last Element: `div(class = "updated", "Last Update: mm/dd/yyyy by FL.")` with mm/dd/yyyy replaced with the date of the update you pushed to the server and FL replaced with your initials.
    + There is no need to use boldface or colons with the section headings when you properly use Heading tags.
2. Pre-requisites--icon: book--Optional
   + If your app needs to ensure that the user has the base understandings necessary to interact with your app, you'll need to create a pre-requisites tab. Otherwise, skip this tab.
3. Activity Tabs--At least one is Required
   + This is the heart of your app. The order of these tabs will depend upon the your goals.
   + Games will use the icon gamepad
   + Explorations will use the icon wpexplorer
4. Last Element: Penn State Logo
   + The bottom of the sidebar should contain the Penn State Logo (see the Penn State Branding section)

### Penn State Branding
Given that we are all associated with Pennsylvania State University, we need to include the Penn State logo in each App. Rather than sticking the logo at the top of the Overview page, we are going to place the logo at the bottom of the sidebar. This has the benefit of having the logo appear throughout the entire app AND making the logo be as unobtrusive as possible in the app.

There are two ways to do this:
1. **CHECK THIS!** Use `boastApp` instead of `shinyApp` from the `boastUtils` package. You won't have to do anything else; the logo will automatically get added in the correct place.
2. In your `ui.R` file, at the end of your `dashboardSidebar()` section, include the following
   ```r
      tags$div(
        class = "sidebar-logo",
        boastUtils::psu_eberly_logo("reversed")
      )
   ```
These methods will ensure that the Penn State logo gets properly used. 

### Mobile Friendly
We want our apps to work well with mobile devices. Thus, when you get to the point where the majority of bugs have been fixed, you need to check how mobile friendly your App is. If you have used `boastApp` and/or the `boast.CSS` file, along with the practices laid out earlier, then you should be well on your way to being mobile friendly.

You can check your App in two ways:

1. Test your App out on a variety of mobile devices
2. Make use of a browser's ability to mimic mobile devices. To do this, launch your App in a browser, then
   + Firefox: Tools --> Web Developer --> Responsive Design Mode
   + Chrome: ???
   + Safari: ???

Look for any issues that you might be able to address before you hand off your App for others to play around with.

### Miscellaneous

## Wording

## Documentation

## Additional Tools
- [lintr](https://github.com/jimhester/lintr) - Checks adherence to a given style, syntax errors, and possible semantic issues.
- [styler](https://www.tidyverse.org/articles/2017/12/styler-1.0.0/) - Format R code according to a style guide.
- [funchir](https://github.com/MichaelChirico/funchir) - stale package check

### Old, Poentially Out of Date Information
- Check potential for mobile friendly --> narrow the window (black block at the bottom?)
- Loading bar to show the process of large number calculation (not needed) 
- Using bsToolTip for silderbar pop over hint, since the regular bsPopover will matach the color code of sider bar 
- Frame around the question of challenges 
- use "i" to open up a short pargraph for instruction; use "?" to open up a hint
 



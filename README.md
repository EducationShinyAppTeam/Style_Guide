Style Guide
================
Neil Hatfield (<njh5464@psu.edu>), Robert Carey (<rpc5102@psu.edu>)
05 May 2020

  - [Writing Code](#writing-code)
      - [Getting Started](#getting-started)
      - [`boastUtils` Package](#boastutils-package)
      - [General Coding Style](#general-coding-style)
      - [Organizing Code](#organizing-code)
      - [Meta Data](#meta-data)
  - [Visual Appearance](#visual-appearance)
      - [Branding](#branding)
      - [Colors](#colors)
      - [Text Styling](#text-styling)
      - [Dashboard](#dashboard)
      - [Mobile Friendliness](#mobile-friendliness)
      - [Miscellaneous](#miscellaneous)
  - [Wording](#wording)
  - [Documentation](#documentation)
      - [References](#references)
      - [Plagiarism](#plagiarism)
      - [`R` Packages](#r-packages)
      - [Graphics](#graphics)
      - [Data](#data)
  - [Accessibility](#accessibility)
  - [Additional Tools](#additional-tools)

This guide spells out the styling that should be used for all apps
included in [BOAST](https://github.com/EducationShinyAppTeam/BOAST).
Styling refers to several different aspects including:

  - How you approaching writing code
  - Visual appearance of the app
  - The wording used in the app
  - Documentation of references, including code and data sources

By following this style guide you’ll ensure that any app you create will
meet our standards.

## Writing Code

### Getting Started

To get started, clone the
[Sample\_App](https://github.com/EducationShinyAppTeam/Sample_App)
template repo found on GitHub. This will provide you with a skeleton for
how to organize your files as well as your code.

**Command Line:**

``` bash
git clone git@github.com:EducationShinyAppTeam/Sample_App.git
```

**Direct Download:**

  - <https://github.com/EducationShinyAppTeam/Sample_App/archive/master.zip>

### `boastUtils` Package

The [boastUtils](https://github.com/EducationShinyAppTeam/boastUtils)
package was created to automate much of the design and development
process. This will not only reduce the amount of work you’ll need to do,
it’ll also make apps more consistent. We **strongly** recommend that you
make use of this tool.

Please check out the package’s
[page](https://github.com/EducationShinyAppTeam/boastUtils) for
instructions on installing and usage.

### General Coding Style

You should adhere to the [tidyverse style
guide](https://style.tidyverse.org/), however, there are some additional
practices you need to follow:

1.  Leave Comments
    
      - At bare minimum, use a comment to break your code into sections.
        These can also provide others with potential keywords to search
        for when looking at your code later on.
      - For particularly complex sections, use comments to summarize
        what you’re trying to do.

2.  Use informative names for variables and functions
    
      - Use names that give another person a sense of what that variable
        represents or what the function is supposed to do. For example,
          - `scoreMatrix` is a matrix that holds a set of scores
          - `checkGame` is a function that checks the state of the
            current game
      - Avoid using the variable names that existed in code you’re
        making use of from another app or script.
          - Don’t use `waitTimes` to hold your data on the number of
            correct answers a user has given.

3.  Format your code
    
      - Use indentation spacing to help make your code readable. RStudio
        has a built-in tool that can help with this.
        
          - Select all of the code you want to reformat. To select all
            code in a file, use Command-A (Mac) or Control-A (Windows).
          - Press Command-Shift-A (Mac), Control-Shift-A (Windows), or
            click on the Code menu and select Reformat Code.
          - NOTE: this tool is imperfect and can result in left
            parenthesis or curly braces moving up a line to where you
            might have an end-of-line comment, resulting in errors.
    
      - Make use of the `styler` and `lintr` packages to help you
        perform formatting checks and to quickly reformat code.
    
      - Be Explicit  
        When passing values to parameters in a function, be explicit and
        include the parameter name in your code. For example,
        
        ``` r
        actionButton(
          inputId = "submit",
          label = "Submit",
          color = "primary",
          style = "bordered",
          class = "btn-ttt"
        )
        ```

4.  Be aware of HTML Tags and how to use them correctly –
    **Accessibility Issue**
    
    HTML Tags should not be used without some basic understanding of
    what that tag is for. Using the tags without such an understanding
    can not only lead to problems with your code running properly or
    looking like what you intended, but can interfere with how
    accessible your app is to wider audience.
    
      - List Items – `tags$li()`
          - All list items need to be enclosed in a larger list
            environment:
              - Use `tags$ol( )` around your items if a user must work
                through the steps in a particular order. This is the
                Ordered List environment.
              - Use `tags$ul( )` around your items if a user can jump
                around the list in any order they wish. This is the
                Unordered List environment.
          - You do NOT need to use Header or Paragraph tags when you’ve
            used a list item tag.
          - Exception to List Environment: the Dashboard Header has a
            built-in listing environment where you do not need to use
            `tags$ol()` or `tags$ul()`.
      - Heading Tags – `h1()`, `h2()`, `h3()`, `h4()`, `h5()`, and
        `h6()`
    
    Heading tags provide a navigational structure to your app. Think of
    them as being the different levels of titles in a book. They are
    **NOT** for making text larger, boldface, or other text styling.
    Think about the headings as laying out a Table of Contents for your
    app, rather than containing content.
    
      - Hierarchy – there is a specific ordering to the header tags. For
        our apps, this would be:
        
          - `h1()` is for the Title of your App and should be ONCE at
            the top of the first page that appears when you load the app
            (i.e., the Overview).
          - `h2()` is for Page titles within the App. These would
            correspond with the tab links you place in the dashboard’s
            left side panel.
          - `h3()` is for titling Sections within a Page of the App.
            These might title the portion of the page that is for a game
            board, questions, answers, and graphs/plots.
          - `h4()` is for a Subsection within a section. You might use
            this to distinguish different sets of controls in a Controls
            section.
          - `h5()` and `h6()` should be used sparingly. These might be
            used for different levels of a game.
    
      - Avoid skipping heading levels
    
      - DO NOT USE headings to style text
    
      - Do not wrap a header tag around a list element (i.e.,
        `h3(tags$li("here is my list item"))`) nor the reverse (i.e.,
        `tags$li(h3("here is my list item"))`)
    
      - Do not mix header tags together in the same line or with the
        paragraph tag.
    
      - For more information check out the [W3C’s
        Tutorial](https://www.w3.org/WAI/tutorials/page-structure/headings/)
    
      - Paragraph Tag – `p()`
    
    Enclose all content text–even if a single sentence–as well as
    equations in a paragraph environment. This tells screen readers what
    the content you’ve created and included in your App is. The
    paragraph tag is what actually gives the structure you defined with
    header tags a body.

5.  Styling Text
    
      - The styling of text (including font size, weight, type, colors,
        etc.) is to be controlled using an **external** CSS (Cascading
        Style Sheet) file.
          - If you are using the `ui.R` and `server.R` format, place the
            following code in the `tags$head( )` portion at the top of
            the `dashboardBody` section of your App:
        <!-- end list -->
        ``` r
        tags$link(rel = "stylesheet", type = "text/css", 
        href = "https://educationshinyappteam.github.io/Style_Guide/theme/boast.css")
        ```
          - If you’re using the `boastApp` function from `boastUtils`,
            you do not need to worry about this; it will automatically
            be done for you.
          - If you need to add additional styling that is *unique* to
            one App, then you will need to create a specific CCS file
            for the App (to be named `[appName].CSS`) and include that
            file in the App’s `www` folder.
              - You will still need to include the above code in your
                `ui.R` file. You will need to duplicate this code but
                alter the `href` to be `[appName].CSS`.
          - If you need additional styling that will impact multiple
            apps, you need to speak with Neil or Bob to see about adding
            to the main CSS file.

6.  Minimize Package Usage
    
      - Make sure that you absolutely have to use a particular package
        before you do. Check to see if what you’re trying to do can be
        done in a package you’re already using or in base R.
      - To help you avoid name masking, ensure that you are actually
        using a package, and to help future readers follow your code,
        explicitly call packages with their functions.
          - For example, use `dplyr::filter([arguments])` instead of
            just `filter([argumens])`.
      - Run a `funchir::stale_package_check` on your `app.R`, `ui.R`,
        and `sever.R` files to see which packages you’re loading might
        not actualy use.

7.  Minimize External Files
    
    Try to minimize the number and size of external files you’re
    attaching to your App. If you’re working on an existing App, remove
    any external files that are no longer necessary.

8.  (*Under development*) Consider using `renderCachePlot` instead of
    `renderPlot`

### Organizing Code

There is a fixed order in which you should write your code. This will
depend on if you are using a singular `app.R` file or the pair `ui.r`
and `server.r`.

#### Using `app.R`

The order for your code will be as follows:

1.  Packages to be loaded
2.  App Meta Data
3.  Any additional source files
4.  UI definition
5.  Server definition
6.  `boastApp` call

#### Using `ui.R` and `server.R`

The order for your code in the `ui.R` file:

1.  Packages to be loaded
2.  App Meta Data
3.  Any additional source files
4.  UI definition

The order for your code in the `server.R` file:

1.  Packages to be loaded
2.  Any additional source files
3.  Server definition

### Meta Data

Each app will need the following meta data in either the `app.R` or
`ui.R` file. For long lines, use the `paste` function to allow you to
break code lines apart but end up with a cohesive string for printing.
This data is used to teach Learning Management Systems (LMS) and
Learning Record Stores (LRS) what your app does. More formats will be
supported in the future.

For now, use the following format:

``` r
## App Meta Data----------------------------------------------------------------
APP_TITLE  <<- "Title of the app"
APP_DESCP  <<- paste(
    "Description of the app",
    "use multiple lines to keep the description legible.",
)
## End App Meta Data------------------------------------------------------------
```

Notice that both `APP_TITLE` and `APP_DESCP` do not follow camelCase.
This is by intent to denote global `constants`.

## Visual Appearance

The visual appearance of each App consists of 6 major areas (plus one
catchall). The benefit of using the `boastApp` function from the
`boastUtils` package is that this will automatically take care of much
of this section for you.

### Branding

Given that we are all associated with Pennsylvania State University, we
need to include the Penn State logo in each App. Rather than sticking
the logo at the top of the Overview page, we are going to place the logo
at the bottom of the sidebar. This has the benefit of having the logo
appear throughout the entire App AND making the logo be as unobtrusive
as possible.

In your `ui.R` file (or your UI section of `app.R`), at the end of your
`dashboardSidebar()` section, include the following

``` r
tags$div(
  class = "sidebar-logo",
  boastUtils::psu_eberly_logo("reversed")
)
```

This will ensure that the Penn State logo gets properly used.

### Colors

The App needs to have a consistent color scheme throughout. The color
scheme should be checked against colorblindness to meet
[WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/) Level AA. You can do
so at the [Coloring for
Colorblindness](https://davidmathlogic.com/colorblind/#%23000000-%23E69F00-%2356B4E9-%23009E73-%23F0E442-%230072B2-%23D55E00-%23CC79A7)
website.

There are two major places where coloring controls come into play: plots
from `R` and the user interface.

#### Plots in `R`

In `R` you can set color theme which you would then use in conjunction
with `ggplot2`:

``` r
# boastPalette is based on the Wong color blind set found at the above website.
boastPalette <- c("#0072B2","#D55E00","#009E73","#ce77a8","#000000","#E69F00","#999999","#56B4E9","#CC79A7")

# psuPalette is based on Penn State's three official color palettes and checked at the above webite.
psuPalette <- c("#1E407C","#BC204B","#3EA39E","#E98300","#999999","#AC8DCE","#F2665E","#99CC00")

# Both palettes get used in the order of what is listed.

g1 <- ggplot2::ggplot(data = df, aes(x = x, y = y, color = grp)) # Create a ggplot object

g1 + scale_color_manual(values=boastPalette)  # If you use "color" in aes
g1 + scale_fill_manual(values=boastPalette)  # If you use "fill" in aes
```

#### User Interface

All aspects of color in the User Interface should be controlled through
the CSS file(s). This includes all of the following:

  - Dashboard coloring (header, sidepanel, main page)
  - Text coloring
  - Coloring of Controls (including, buttons, sliders, and other input
    fields)

By using CSS, especially through `boastApp`, you’ll be able to ensure
that there is consistent coloring throughout your App.

### Text Styling

Text styling refers the non-content aspects of the text on the page.
This means things such as the use of italics, boldface, alignment, as
well as font size and color.

You should let the `boast.CSS` file do the heavy lifting setting up the
styling. (Again, using `boastApp` will help you.) However, you will need
to tag content appropriately.

#### Headings

Use the Heading Tags for the short fragments that define the structure
of your app. If you find yourself enclosing a complete sentence in
Heading tag, you ARE NOT using headings correctly. Notice how the
headings in this Style Guide aren’t complete sentences; your App should
mimic this. Full sentences appear as regular paragraph text (i.e.,
enclosed in `p()`).

#### Paragraph Text

If you enclose text that gives instructions or other information to your
app’s users in `p()` or `li()`, your App will understand how to style
that text correctly. The `boast.CSS` file contains controls that set the
base font size much larger than shiny does natively as well as making
the text dynamically for mobile devices and screen sizes. Again, using
`boastApp` makes this process easier.

If you want to make a certain word or phrase italic, you will need to
wrap that text in `tags$em()`. Similarly, if you want do the same with
boldface, you’ll use `tags$strong()`.

For example, this code:

``` r
p(
  "When dealing with the ",
  tags$em("t"),
  "-distribution, we only have one parameter, the ",
  tags$strong("degrees of freedom"),
  "that we need to input."
)
```

Becomes:

When dealing with the *t*-distribution, we only have one parameter, the
**degrees of freedom** that we need to input.

Use italics/emphasis, and boldface/strong sparingly.

#### Mathematics

For the most part, any mathematics you need displayed should be done
using [MathJax](https://www.mathjax.org/). Default to using inline
typesetting with the `\\(` and `\\)` delimiters. If you need to use
display style, you can use `\\[` and `\\]` or double dollar signs. For
the vast majority of mathematics, you’ll wrap both inline and display
style mathematics inside of a paragraph environment.

If you’re writing mathematics directly in your app, remember you’ll need
to escape the LaTeX commands by putting an extra \\ in front; e.g.,
`\frac{3}{4}` would need to be `\\frac{3}{4}`.

If you’re reading in mathematical text from an external CSV file, you do
not need the extra backslash in the CSV file.

**Note:** Double dollar sign delimiters are generally not recommended
for displaying math as they can lead to unintended results. See:
[Writing Mathematics for
MathJax](https://docs.mathjax.org/en/latest/basic/mathematics.html).

#### \[Game\] Question Text

The text used as a question in a game should NOT be wrapped in a Heading
tag; wrap the text in a paragraph tag.

#### Label Text (Buttons, Sliders, Other Inputs and Alerts)

If you are using the `boast.CSS` file, the text that is included in/on
buttons, dropdown menus, sliders, radio buttons, choices, and other
inputs as well as alert messages and popups/rollovers, will
automatically be styled correctly.

Do not use heading tags, the paragraph tag, italics/emphasis, or
boldface/strong with input labels.

You may use these tags with popups/rollovers.

#### Feedback and Hint Text

Again, let the `boast.CSS` file handle the styling of this type of text.

#### Text in `R` Plots

Unfortunately, text in `R` plots do not get controlled by CSS. This
means that you’ll have to play around with the settings. Using the
`ggplot2` package to make your plots (or other packages based upon the
ggplot framework) will allow you to use the `theme` aspect to control
text in your App.

Here is an example for how to do this:

``` r
g1 <- ggplot2::ggplot(data=df, aes(x=x, y=y, color=grp)) #create a ggplot object

g1 + theme(
  plot.caption = element_text(size = 18),
  text = element_text(size = 18)
)
```

You will need to play around with the settings to find the appropriate
value; text size 18 does appear to work out well.

### Dashboard

The ordering of the Tab Pages for your App should make logical sense and
should structure how you want users to use your App. Additionally, we
have specific icons that should be used with particular Tab Pages.

1.  Overview–icon: Dashboard–**REQUIRED**
      - This tab page is required for all Apps. This is the main landing
        page of your App and should appear at the top of the sidepanel.
    
      - Will contain the following elements
        
        1.  “Title” (as Heading 1)
        2.  A description of the app (as paragraph text under the title)
        3.  “Instructions” (as Heading 2)
        4.  A list of instructions (using an Ordered List environment)
        5.  A button that will take the user to the next page.
        6.  “Acknowledgements” (as Heading 2)
        7.  A listing of acknowledgements including, coders, content
            writers, etc. (as a paragraph)
        8.  Last Element: `div(class = "updated", "Last Update:
            mm/dd/yyyy by FL.")` with mm/dd/yyyy replaced with the date
            of the update you pushed to the server and FL replaced with
            your initials.
    
      - There is no need to use boldface or colons with the section
        headings when you properly use Heading tags.
2.  Pre-requisites–icon: book–Optional
      - If your app needs to ensure that the user has the base
        understandings necessary to interact with your app, you’ll need
        to create a pre-requisites tab. Otherwise, skip this tab.
3.  Activity Tabs–At least one is Required
      - This is the heart of your app. The order of these tabs will
        depend upon the your goals.
      - Games will use the icon gamepad
      - Explorations will use the icon wpexplorer
4.  Last Tab Element: References–icon: leanpub–REQUIRED
      - This page is where you will place a reference list for all of
        the following items that you used in your app:
          - All `R` packages you used
          - Sources of Code you used directly or drew heavily upon
          - Pictures and/or other images
          - Data sets
      - Refer to the Documentation Section of this Style Guide for more
        information
5.  Last Element: Penn State Logo
      - The bottom of the sidebar should contain the Penn State Logo
        (see the Penn State Branding section).

### Mobile Friendliness

We want our apps to work well with mobile devices. Thus, when you get to
the point where the majority of bugs have been fixed, you need to check
how mobile friendly your App is. If you have used `boastApp` and/or the
`boast.CSS` file, along with the practices laid out earlier, then you
should be well on your way to being mobile friendly.

You can check your App in two ways:

1.  Test your App out on a variety of mobile devices.
2.  Make use of a browser’s ability to mimic devices. To do this, launch
    your App in a browser, then enable one of the following:
      - [Chrome: Device
        Mode](https://developers.google.com/web/tools/chrome-devtools/device-mode/#viewport)
      - [Firefox: Responsive Design
        Mode](https://developer.mozilla.org/en-US/docs/Tools/Responsive_Design_Mode)
      - [Microsoft Edge: Device
        Emulation](https://docs.microsoft.com/en-us/microsoft-edge/devtools-guide/emulation)
      - [Safari: Responsive Design
        Mode](https://support.apple.com/en-gb/guide/safari-developer/dev84bd42758/mac)

Look for any issues that you might be able to address before you hand
off your App for others to play around with. Assign a **Mobile
Friendliness Rating** to your app on a scale from 1 to 5.

1.  Not functional
2.  Functional – Very awkward
3.  Functional – Okay if no big screen available (multiple issues)
4.  Usable in a small class setting (single issue)
5.  Readily usable

### Miscellaneous

  - Consider adding a loading bar to show the process of large number
    calculations.

## Wording

When writing the content for your App, you will want to keep in mind
that these Apps have the primary audience of students. Thus, we need to
make sure that we use language that is appropriate. Seek to use complete
sentences that convey what you intend. Have someone else take a look at
your content and then tell you what they believe the text to be saying.
If what they say is consistent with what you intended, great. If not,
then you need to revise your text.

**DO NOT sacrifice clarity and precision/accuracy for
conciseness/brevity.**

Since these Apps are for *teaching*, we need to use language that is
accurate and supports students in constructing productive meanings. This
means that we need to avoid sloppy language and re-enforcing problematic
conceptions. For example,

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

## Documentation

These Apps are the product of your hardwork and are part of your
academic record. Thus, you need to adhere to [Penn State’s Academic
Integrity
Policy](https://undergrad.psu.edu/aappm/G-9-academic-integrity.html).
This is especially important as we are making the Apps available through
a Creative Commons Attribution-ShareAlike 4.0 International license ([CC
BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)). If you
have used code, pictures, data, or other materials from outside of the
BOAST team, you **MUST** give proper credit. These references will then
be included on the App’s References page.

### References

All Apps will need a References Tab. This is where you’ll place all
references for your App, including R packages, borrowed code, data
sources, images, etc. This in addition to the Acknowledgements. (NOTE:
listing something in the Acknowledgements DOES NOT waive this
requirement.)

You may use any citation style you wish, but be consistent. Recommended
citation styles include APA and AmStat. Here is a starting code block
for you to use:

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

**You MAY NOT use blocks of code you’ve found online without giving
proper attribution.**

There is a difference between looking at example code online to see how
to do something and copying that code directly. The former is
permissible, the later is plagiarism. + If you want to use someone
else’s code “as is” (without any changes), you should reach out to the
author for permission first. + If you use someone else’s code and make
modifications, you need to give credit to where you got the code, and
potentially ask for permission.

You will need to place citations in ***two*** places: in the References
Tab Page and in your code.

#### Reference Tab Page

Use the following format:

Author. (Date). Title of program/source code (Version number, if
applicable). \[type of code\]. Retrieved from \< URL \>.

For example,

Hatfield, N. J. (2017). First day activity (v1). \[Netlogo\]. Retrieved
from <https://neilhatfield.github.io/statApps/Day1Activity.html>.

#### In Code

Use the following format in your code to cite where you got the code
from.

``` r
#-----------------------------------------------------------------------------------------
#    Title: <title of program/source code>
#    Author: <author(s) names>
#    Date: <date>
#    Code version: <code version>
#    Availability: <where it's located>
#-----------------------------------------------------------------------------------------
# [reused code then follows]
# ...
# [last line of reused code]
#End of <author>'s code-------------------------------------------------------------------
```

### `R` Packages

If you made use of any packages in `R`, then you will need to add these
to the Reference subsection. Fortunately, there is a built-in tool that
will help you: the `citation` function. In R (RStudio) simply type
`citation("packageName")` and you’ll get the appropriate citation
information for the package you used. For example,
`citation("shinydashboard")` and `citation("plyr")` will give the
information needed for the following citations:

Chang, W. and Borges Ribeio, B. (2018). shinydashboard: Create
dashboards with ‘Shiny’. (v0.7.1) \[R Package\]. Available from
<https://CRAN.R-project.org/package=shinydashboard>

Wickham, H. (2011). The Split-apply-combine strategy for data analysis.
Journal of Statistical Software, 40(1). pp. 1-29. Available at
<http://www.jstatsoft.org/v40/i01/>.

Notice, that the format of the R package will depend on whether there is
an article published for the package. The `shinydashboard` package is
not associated with an article while the `plyr` package is associated
with Wickham’s article.

### Graphics

Pictures, drawings, photographs, images, etc. are typically copyrighted.
When you’re selecting images, make sure that the images are Open
Source/Copyright Free/Royalty Free/Public Domain. Additionally, include
a reference to where the pictures came from in the Overview Page. The
basic format to use is:

LastName, First Initial. (Year). Title of artwork. \[Format\]. Retrieved
from \< URL \>.

### Data

If you are using any data files, you need to attribute where those files
are coming from in the References subsection of your Overview page. A
suggested formats to use is:

Author/Rightsholder. (Year). Title of data set (Version number)
\[Description of form\]. Location: Name of producer.  
Author/Rightsholder. (Year). Title of data set (Version number)
\[Description of form\]. Retrieved from <http://www.url.com>

If you (or someone else) had to sign some type of agreement to access
the data, we must examine the agreement before you make your App
publicly accessible. Just because you got access to the data does not
mean you have the right to share the data.

## Accessibility

We need to make sure that our Apps are accessible. If you have been
adhering to the style guide, your App should be in a decent position.
When you’re ready to test the accessibility of your App, you’ll need to
deploy the App to a sever and then use the [WAVE Web Accessibility
Evaluation Tool](https://wave.webaim.org/). Enter the URL of your App in
the noted box to run an evaluation. See what accessibility issues your
App has and then address them.

**See:** + [Accessibility and Usability at Penn
State](https://accessibility.psu.edu/) + [Accessibility
Statement](https://www.psu.edu/accessibilitystatement) + [How to Meet
Web Content Accessibility
Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)

## Additional Tools

  - [lintr](https://github.com/jimhester/lintr) - Checks adherence to a
    given style, syntax errors, and possible semantic issues.
  - [styler](https://www.tidyverse.org/articles/2017/12/styler-1.0.0/) -
    Format R code according to a style guide.
  - [funchir](https://github.com/MichaelChirico/funchir) - stale package
    check

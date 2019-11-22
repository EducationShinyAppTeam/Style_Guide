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
Ultimately, when you write your app's code, you should adhere to the [tidyverse style guide](https://style.tidyverse.org/). However, here are some additional practices you should follow.

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
4. Be aware of HTML Tags and use them correctly--__Accessibility Issue__
    HTML Tags should not be used without some basic understanding of what that tag is for. Using the tags without such an understanding can not only lead to problems with your code running properly or looking like what you intended, but can interfere with how accessible your app is to wider audience.
    1. List Items--`tags$li()`
        + All list items need to be enclosed in a larger list environment:
            - Use `tags$ol( )` around your items if a user must work through the steps in a particular order. This is the Ordered List environment.
            - Use `tags$ul( )` around your items if a user can jump around the list in any order they wish. This is the Unordered List environment.
        + You do NOT need to use Header or Paragraph tags when you've used a list item tag.
        + Except to Environment:  the Dashboard Header has a built-in listing environment where you do not need to use `tags$ol()` or `tags$ul()`.
    2. Header Tags--`h1()`, `h2()`, `h3()`, `h4()`, `h5()`, and `h6()`
        Header tags provide a navigational structure to your app. Think of them as being the different levels of titles in a book. They are __NOT__ for making text larger, boldface, or other text styling. Think about the headings as laying out a Table of Contents for your app, rather than containing conent.
            1. `h1()` is for the Title of your App and should be ONCE at the top of the first page that appears when you load the app.
            2. asd


## Visual Appearance

## Wording

## Documentation

## Additional Tools
- [lintr](https://github.com/jimhester/lintr) - Checks adherence to a given style, syntax errors, and possible semantic issues.
- [styler](https://www.tidyverse.org/articles/2017/12/styler-1.0.0/) - Format R code according to a style guide.

### Apps
- Format the page using the consistant color
- Check potential for mobile friendly --> narrow the window (black block at the bottom?)
- Matching game by input the letter
- First tab --> Prerequisite page-- (providing information on statistics)
- Second tab --> About pages: a) about statement b) instruction c) acknowledgement --> bold, colon  
- Hint: question mark on the upper left of each page 
- Feedback --> given according to the user's input 
- Loading bar to show the process of large number calculation (not needed) 
- Using header on the top for different levels game
- Using bsToolTip for silderbar pop over hint, since the regular bsPopover will matach the color code of sider bar 
- Frame around the question of challenges 
- use "i" to open up a short pargraph for instruction; use "?" to open up a hint
- Put PennState logo on the About page, link to Stat department or school website. Use the square logo!  



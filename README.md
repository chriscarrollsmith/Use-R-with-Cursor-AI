# How to Use R in Cursor: The AI-First Code Editor

For the most part, the R programming language ecosystem assumes you are using RStudio or Positron as your IDEs. It is possible, however, to use R in other editors, including VSCode and VSCode forks like Cursor, the AI-native IDE. Unfortunately, the Cursor team has left some features of the R language extension in a broken state, so you won't currently be able to get syntax highlighting or tooltips for R in Cursor. With that said, however, Cursor's powerful interface for AI coding workflows makes up for this shortcoming to a great extent, and you may be surprised just how much Cursor can accelerate your R coding productivity. Want to give it a try? This guide will show you how to set up Cursor to use R.

If you prefer video explainers, you can also see my YouTube video, which covers the same material:

[How to Use R in Cursor: The AI-First Code Editor](https://youtu.be/ewtM44f5IjQ?si=JbkPlhNmfFqr3hwY)

## Setup

Step 1. Install R for your operating system from [CRAN](https://cran.r-project.org/).
1. Go to the official R website (https://www.r-project.org/).
2. Download the appropriate version for your operating system.
3. Run the installer and follow the prompts.

Step 2: Install [Cursor IDE](https://cursor.com/)
1. Visit the Cursor website (https://cursor.com/).
2. Click on the download link, which should automatically detect your operating system.
3. Once downloaded, run the installer.

Step 3: Install [Pandoc](https://pandoc.org/installing.html) for your operating system
1. Visit the Pandoc website (https://pandoc.org/).
2. Go to the "Installing" tab.
3. Choose one of the following methods:
  a. Download and run the installer directly.
  b. Use a package manager:
    - Windows: Use Scoop or Chocolatey
    - macOS: Use Homebrew
4. If using a package manager, open a terminal and run the appropriate command:
  - Scoop: `scoop install pandoc`
  - Homebrew: `brew install pandoc`
5. Verify the installation by running `pandoc --version` in the terminal.
6. Restart your computer to ensure Pandoc is properly recognized.

Step 4: Install [R tools](https://cran.r-project.org/bin/windows/Rtools/) (Windows users only)
1. Go to the CRAN R project website.
2. Find the R tools page.
3. Download and run the R tools installer.

Step 5. Install [Quarto CLI](https://quarto.org/docs/get-started/) for your operating system.
1. Go to the Quarto website (https://quarto.org/).
2. Download the appropriate version for your operating system.
3. Run the installer and follow the prompts.

Step 6: Install and configure Cursor extensions
1. Open Cursor IDE.
2. Toggle the primary sidebar using the button in the upper right corner.
3. Click on the "Extensions" tab.
4. Search for "REditorSupport" in the search bar.
5. Install the [R extension](https://marketplace.visualstudio.com/items?itemName=REditorSupport.r).
6. Click on the gear icon next to the installed R extension and select "Extension Settings."
7. Enable the following settings:
  - R: Use Renv (if you plan to use renv for environment management)
  - R: Plot Use HTTPGD
8. Install the [Quarto extension](https://marketplace.visualstudio.com/items?itemName=quarto.quarto) by searching for it in the Extensions tab and clicking "Install."

Step 7: Set up R environment and dependencies
1. Open a new terminal from the "Terminal" menu in Cursor.
2. Clone the GitHub gist with R setup commands:
  ```
  git clone https://gist.github.com/chriscarrollsmith/88d7dc3b4ac5255c4d7fb7f180fa72eb.git
  ```
3. Navigate to the cloned folder:
  ```
  cd 88d7dc3b4ac5255c4d7fb7f180fa72eb
  ```
4. Open the `Rconfig.R` file:
  ```
  code Rconfig.R
  ```
5. Run the script by clicking "Run Source" or using the appropriate keyboard shortcut.
6. Wait for all packages to install (this may take a few minutes).
7. Restart R to ensure all libraries are properly loaded.

## Usage

Step 1: Create an R project in Cursor
1. Create a new project folder.
2. Open the folder in Cursor.
3. Create a new file with an `.R` extension.

Step 2: Use AI-assisted coding
1. In your R file, press `Ctrl+K` to bring up the AI prompt box.
2. Select your preferred AI model (e.g., Claude 3.5 Sonnet).
3. Enter a prompt (e.g., "Write me a ggplot demo in R").
4. Click "Generate" to create the code.

Step 3: Run and view plots
1. Wrap your plots in `print()` statements to ensure they display in Cursor.
2. Run the code to generate and view the plots.

Additional Tips:
- Use tab completion to accept code suggestions.
- Highlight code and click the "Chat" button to add code snippets to AI chat and ask for explanations or modifications.
- Construct your custom chat context by adding files to the chat with the `+` button or even pasting in a link to documentation (which will be automatically scraped and pulled into the chat).

## A note on project-level environments

It's generally good practice to use the [renv](https://rstudio.github.io/renv/articles/renv.html) package to manage dependencies at the project level rather than installing them directly into the user library. This makes project environments more reproducible and reduces dependency conflicts. However, Cursor depends on some R packages to provide R language support, and these unfortunately become unavailable when `renv` is used. So you will probably need to install `jsonlite`, `languageserver`, and `httpgd` manually in every project. 

In theory you should be able to solve this by manually adding your user library to the project `.libPaths()` with `.libPaths(file.path(Sys.getenv("USERPROFILE"), ".R/library"))`, and there is even a setting in the R language extension settings to automate this, but I haven't been able to get this workaround to work. Probably this is just an annoyance you'll have to live with if you want to use Cursor with `renv`.
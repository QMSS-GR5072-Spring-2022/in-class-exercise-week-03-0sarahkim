# In-class-exercise repo

This repository contains an `.Rmd` notebook with starter code to facilitate following the material covered in class. You are expected to:
* work on the notebook during the class, and add your own notes and experiments with code
* create a GitHub-flavored `.md` file and `push` it along with your annotated `.Rmd` file at the end of the class

#### Follow the steps below:

1. select a location in your machine where you'll `clone `this repo
```
$ cd <your selected location here>
```

2. copy the url for this repo, and `clone` it to the current location
```
$ git clone <paste-your-url>.git
```

3. follow the class using the `.Rmd` notebook included in this repo, and add your notes where appropriate

4. at the end of the class, `knit` your `.Rmd` notebook to create a GitHub-flavored `.md` file, and place this file in a new directory called `notebooks\` so that the final repo follows the below structure:
```
repo\
 | -- .gitignore
 | -- README.md
 | -- src\
 		| -- in-class-exercise-notebook.Rmd
 | -- notebooks\
 		| -- in-class-exercise-notebook.md
```

4. at the end of the class, take the usual steps to `push` these files back to the repo
```
$ git add <your-new-files-here>
$ git commit -m "<your-message-here>"
$ git push -u origin main
```

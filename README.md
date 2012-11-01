css-build-hook
==============

A basic git pre-commit hook to concatenate and minify all css and save to a new location so you still have a working copy.

Firstly you will need to download the YUI compressor.

	http://yuilibrary.com/projects/yuicompressor/

Test this is in the correct location and working by running. Changing the location of your YUI jar and the style sheets.

	java -jar ~/bin/yuicompressor.jar ~/path/to/styles/styles.css -o ~/path/to/styles/builds/styles-min.css

Check that you now have a new minified stylesheet in your desired location.

Now within your repo add the pre-commit file to .git/hooks/ or if you already have a pre-commit hook just add the contents to your existing file.

Change the path of the following to your desired locations and file names.

	CSS_DIR="styles/"

	CSS_BUILD_FILE="$CSS_DIR/builds/style-min.css"

If you want your minified file to be in a different location to your working copy you can use the following snippet to check that the location exists before trying to write to it.


	if [ ! -d "$CSS_DIR/builds" ]; then
	    cd $CSS_DIR
	    mkdir builds
	    cd $GIT_ROOT
	fi

I found that the "cat" command takes the files in alphabetical order so if you have anything like a css reset file please make sure this is first in the list. Also if you just want to minify files and not concatenate or you only have one file you can remove this section.

This is a very basic example which could easily be expanded but for the small project I used it on it worked fine.



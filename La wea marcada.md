![pcel_logo](https://images.pcel.com/static/data/logo2.gif)

#Guide for coding 
####Documentation, code style and all the general info for a good code

> **Description**: This file provides help for code documentation, code styling, commits, and others, so we can have a nice code and others devs can understand what our code does easily. 

For intern documentation the system use the `PHP Documentor` syntax wich can be found here:  [PHPDocumentor Site](https://www.phpdoc.org/). Also we require some extra documentation which is not parsed to the documentation files but is required just in case some developer needs to know what does a piece of code.

The minimum requirements for a good documentation are:

>  - File
>  - Classes
>    - Vars for the class
>  - Functions
>    - Parameters
>  - Special code

All the documentation needs to be in english, not in spanish with small and clear sentences, for example:

    <?php
	/**
	* ...
	*/
	class Example 
	{
	
	    /**
	    * Script version
	    * @var int
	    */
	    private $version = 1;

In this way, the PHP Documentor knows almost everything required from the variable and the developers can easily check the variable in the documentation instead of reading the code. You can include more documentation if you want based on the PHP Documentator syntax.

Here is an example of a wrong documentation based on the last example:


    <?php
    /**
    * ...
    */
    class Example 
    {
   
	    /**
    	* This var stores the project version so we can use it when we want to test the version
    	* @var int
    	*/
	    private $version = 1;

Also if there are some errors in the documentation and is pushed to `master` then, the project will be broken in the documentation, because the documentation is parsed from `master` not from every branch, so the developer needs to test if the documentation is being parsed without errors or there are bugs.

For testing documentation you can do it in only one file or in all the project using the phpdoc command in CLI with a simple command. This command parse a directory (using `-d`)  and test the project sending the result to the `-t` path.

    phpdoc -d /path/to/files/ -t /path/to/docs/ 
If we want to test only one file we can use the `-f` option instead of `-d` and the path to the file. So we can test if our documentation is parsing without errors or there are some errors wich needs to be fixed.

Here is a *full* example of the workflow we need to do for documentation

 1. First we write the code to solve the problem or requirement.
 2. We test it so we know our code works as intended.
 2. Then, we document the main code (check minimum requirements to know what is the main code)
 3. We check the code again and adds extra documentation just in case is required
 4. We test the documentation running the `phpdoc` command 
 5. If everything is okay, we push it to the branch as a commit, in case we need multiple commits then, we just test the documentation on the last commit because we only need the documentation on the last commit which is going to be merged to  `master`.
 6. That's it!


----------

#Code styling

For code styling we can check the project `pcel.com` @ https://github.com/pcel/pcel.com and check the `readme`.

We also recommend, try to use the PSR styling (0, 1, 2, 3 and 4) which can be found here:

 - https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
 - https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
 - https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
 - https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-3-logger-interface.md
 - https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md

Those coding standards can help the developers to read more easily our code and then, learn the way it works in less time. 

For example (a simple code without PSR rules applied correctly and without documentation, but with a good code styling):

    <?php

	class Example
	{
	
		private $something = "Hello";
		
		public function __construct(){}

		public function saySomething()
		{
			return $this->myWorld($this->something);
		}

		private function myWorld($something)
		{
			if($something === "Hello") {
				return "Hello world";
			} else {
				return "Good bye world";
			}
		}

	}

And a wrong example of code styling (without PSR/documentation):


    <?php
	class Example{
	private $something = "Hello";
		
		public function __construct(){
	}public function saySomething(){			return $this->myWorld($this->something);
		
		}
			private function myWorld($something){
			if($something === "Hello") {
		return "Hello world";
						} else {				return "Good bye world";
			}
		}

	}

As we can see we can read more easily the first code, because the second is not having a good code styling.

Also, if we don't need some code, just remove it like commented lines that are not used in the script, for example:

    //$var = "something";
    $var = 2;
As we know $var is going to be 2 not "something" so we don't need to have that comment in our code. 

Also for example if we don't need a var try to avoid them, like:

    $var = 1;
	if($array[$var] === 1)
		echo "Its 1";
We can just do \$array[1] instead of \$array[$var] because we don't need that var so our code is more clean and more efficient.

Finally, an important part of the code style is using functions with less than 13 code lines (excluding comments) so the code complexity is low, for example a good function is (not using rules from this doc, just as a fast example):

    function fooBar($foo){
	    //this line doesn't count in our "13 code lines"
	    $thisLineCountAs = 1; //1 line
	    for($i = 0; $i < 13; $i++){ //2 line
			switch($i){ //3 line
				case 1: //4 line
					echo "Its a baby!"; //5 line
				break; //6 line
				case 2: //7 line
					echo "Now its an adult!"; //8 line
				break; //9 line
			}//10 line
		}//11 line
		//this line doesn't count too
		sayHi(false); //12 line, If we don't use another function our code is 13+ lines
	}
	//this function is only 4 lines
	function sayHi($bool){
		if($bool === TRUE) {
			echo "Hi!";
		} else {
			echo "Good bye!";
		}
	}


----------


#Unit tests

We are not doing unit tests right now...nor Travis or any other testing


----------


#Commits

Basic information:
https://github.com/pcel/pcel.com#commit-messages

Commits requires a good title and a good description, so the developers know what changes you did in the code (logic, renaming functions/clases/variables, typos, and others), so your title needs to be descriptive but small, for example:

> Search engine update

So in first, as we can read in slack, we know the search engine was changed, but what changes, why, requires testing, feedback or something?...We can check the code and do a basic review, for example on a query like:

From:

    SELECT * FROM something WHERE column = 1;

To:

    SELECT * FROM something WHERE column = 1 AND category = 25;

As we can check we know the query nows select the category 25, but, why?, what is that category?. We can add a commit description so the developers know what changes, why, and all the info we can give them in our commit description.

Rules for a good commit:

 1. Separate subject from body
 2. Limit the subject line to 50 characters
 3. Capitalize the subject line
 4. Do not end the subject line with a period
 5. Use the imperative mood in the subject line
 6. Wrap the body at 72 characters
 7. Use the body to explain what and why vs. how

Try to avoid commits wich are not required, we know sometimes we want to change the branch, and we had changes so we need to push them as "_minor changes_", but try to avoid them, and don't create commits with a lot of changes in the code, try to know when to commit changes. For example:

You changed like 10 files and a lot of code. That's an example of a bad practice because the developer now need to check 10 files and a lot of code and that requires more time to understand the changes and if they want to recover some code or want rollback that commit maybe other changes can be losed.

You changed the style of a page, changing .css and some .html code, then, that's time for a commit like:

> Title: Changed the header bar
> Autor: Root
> Time: 01-01-1900 @ 10:00:00 am
> Branch: headerFix
> Repo: pcel.com
> Description: The header bar had a bug in the search input style. Requires clear the cache in dist.

Obviously we don't include "autor, time, branch, repo" only title as the commit title and description as the commit description.


----------


#Branches

Right now there is a mess with the code because all of the scripts that requires support and are being worked by multiple developers, for example, if pcel.com requires changes in style, the developer A is working on the .tpl files, at the same time, requires changes in backend, the developer B is working on the .php files. As we know there is no problem if we commit both files in the same branch, but in real life doing this way we need to do the common line: "pull, commit, push" always, and maybe the other dev can have issues doing pull because we can generate conflicts if we both changed the same file, or we can remove our code by mistake doing that.

For _fixing_ that, we can use branches, for example branch: _headerFix_ and branch _filterChanges_ and work without problems in our branches, then, just merge them. If we have any conflicts is more easy to just fix them in the merge than doing it every commit...

So, try to work in branches, wich can be reviewed and then merged to `master` more easy.

----------


#Useful links

 - https://www.sitepoint.com/introduction-to-phpdoc/
 - https://www.phpdoc.org/docs/latest/index.html
 - https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
 - https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
 - https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
 - https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-3-logger-interface.md
 - https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
 - http://www.php-fig.org/
 - http://flowframework.readthedocs.io/en/stable/TheDefinitiveGuide/PartV/CodingGuideLines/PHP.html
 - http://chris.beams.io/posts/git-commit/

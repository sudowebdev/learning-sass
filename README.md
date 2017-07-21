# SASS/SCSS

## What is SASS?
Sass is a **CSS pre-processor**. So, the question now becomes: **What is a CSS pre-processor?**

### What is a CSS pre-processor
A CSS pre-processor is a **scripting** language that **extends CSS** by allowing developers to write code in one language and then compile it into CSS. Some examples of CSS pre-processors include: ***Sass, Less and Stylus***.

## What is SCSS? Is it the same as SASS?
When Sass first came out, the main syntax was **noticeably different** from CSS. It used indentation instead of braces, didn't require semi-colons and had shorthand operators.

Some folks didn't like the variation in syntax. So, SCSS came into sight which has a CSS like syntax. 

The difference can be summarised as:
1. **SCSS (Sassy CSS)**: Uses the .scss file extension and is fully compliant with CSS syntax
2. **Indented (simply called 'Sass')**: Uses .sass file extension and indentation rather than brackets; it is not fully compliant with CSS syntax, but it's quicker to write																	
I'll be writing in SCSS syntax, because that is what I prefer.

## Installation

All the installation instructions are clearly written **[here](http://sass-lang.com/install)**.  
I'll be using **Koala** (see inside the Applications tab), since I want to keep this tutorial **focused on learning SASS/SCSS** and not on their installation.


Without any further ado, lets get our hands dirty.

&nbsp;
# SASS/SCSS guide 

## Variables

Yup, variables. **SCSS brings variables to CSS**.  

Acceptable values for variables include numbers, strings, colors, null, lists and maps.  

Variables are defined using the **$** symbol.

	$primaryColor: blue;

##### Please Note: All the respective codes are placed in the respective files. For instance: the code that relates to variables is put inside variables.scss.	


### Scope of variables

Now, just like variables defined in any other language, Sass variables also have scope. This means if you declare a variable within a selector, it is then scoped within that selector.

Check this one out:  

	$primaryColor: blue;

	body {
		$primaryColor: green;
		background-color: $primaryColor;
	}

	p {
		color: $primaryColor;
	}

Compile this and check the **color** property of **p selector**.





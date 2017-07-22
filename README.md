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

##### Please Note: All the respective codes are placed in the respective files. For instance: the code that relates to variables is put inside styles/variables/variables.scss.	


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

### !global flag 

But wait!  
What if we want to set a variable **global from within a declaration**. In that case, we have to use **!global** flag.  


	$secondaryColor: green;

	div {
		$secondaryColor: blue !global;
		background-color: $primaryColor;
	}

	span {
		color: $primaryColor;
	}


### !default flag

This flag is used for providing a default value for a variable. If a value is provided, it is overwritten:

	
	$firstValue: 62.5%;

	$firstValue: 24px !default;

	body {
		font-size: $firstValue;
	}

	// body font size = 62.5%


## Math

Sass allows us to use **mathematical expressions**. This can be super useful in case of **assigning dimensions to selectors that are dependent on dimensions used by other selectors**.


Supported operators include:
	
**"+"** 	Addition  
**"-"** 	Subtraction  
**"/"** 	Division  
**"*"** 	Multiplication  
**"%"** 	Modulo  
**"=="** 	Equality  
**"!="** 	Inequality 


There are 2 cases which you have to keep in mind before using Math expressions in your Sass files. These are: 

<ul>

<li> First, because the **/** symbol is used in shorthand CSS font properties like font: 14px/16px, if you want to use the division operator on non-variable values (Variable values are values which involve variables. For instance: $fontDiff = $font/15px), you need to wrap them in parentheses like: 

	$fontDiff: (14px/16px);

</li>

<li> Second, you can't mix value units:

	$container-width: 100% - 20px; //error

</li>

The above example won't work. Instead, for this particular example you could use the css calc function, as it needs to be interpereted at render time.

</ul> 


	$container-width: 100%;

	.container {
	  width: $container-width;
	}

	.col-4 {
	  width: $container-width / 4;
	}


## Functions

The coolest part about Sass is its built-in functions. The full list can be explored here -> **[Functions in Sass/Scss](http://sass-lang.com/documentation/Sass/Script/Functions.html)**


## Nesting

Now, Sass also provides us with the feature of **nesting declarations**. What that means is that now we can have a **declaration inside of another declaration**.  

Makes sense?  
**Let's switch back to code!**  

In **CSS**, we can **perform nesting** like this: 

	
	.container {
	    width: 100%;
	}

	.container h1 {
	    color: red;
	}


But in **Sass/Scss** we can get the **same result** by writing:

	
	.container {
	    width: 100%;
	    h1 {
	        color: red;
	    }
	}

Which one sounds more **intuitionistic**? You got the answer!


### Reference the Parent (& operator)

Sass also gives us a way to reference the parent in case of nesting.

		
	a.myAnchor {
	    color: blue;
	    &:hover {
	        text-decoration: underline;
	    }
	    &:visited {
	        color: purple;
	    }
	}

### De-nesting (@at-root directive)

Sass also helps us in de-nesting if we want to. So, if we have written something like this: 

	
	.first-component {
	    .text { font-size: 1.4rem; }
	    .button { font-size: 1.7rem; }
	    .second-component {
	        .text { font-size: 1.2rem; }
	        .button { font-size: 1.4rem; }
	    }
	}

After sometime, if we want to de-nest .second-component, we can use **@at-root**: 

	.first-component {
	    .text { font-size: 1.4rem; }
	    .button { font-size: 1.7rem; }
	    @at-root .second-component {
	        .text { font-size: 1.2rem; }
	        .button { font-size: 1.4rem; }
	    }
	}   


	/*

	generated CSS looks like this

	.first-component .text {
	  font-size: 1.4rem;
	}
	.first-component .button {
	  font-size: 1.7rem;
	}
	.second-component .text {
	  font-size: 1.2rem;
	}
	.second-component .button {
	  font-size: 1.4rem;
	}

	*/


### Some more info on Nesting

**Already loving it**? Well, nests are a really great way to **save some time** and **make your styles readable** but over-nesting can cause **problems** with overselection and filesize.  

So, the **rule of thumb** is to: 
>Always look at what your Sass/Scss compiles to and try to follow the "inception rule"

##### Inception Rule
>Don’t go more than four levels deep.


## Imports

**Imports** allow you to **break your styles** into **separate files** and **import** them into one another.   


We can import a .scss file using the **@import** directive:

	@import "grids.scss";

In fact, you **don't** even really need the extension:

	@import "grids";


## Partials

Sass also include a concept called **partials**. If you **prefix** a .sass or .scss file with an **underscore**, it will **not get compiled to CSS**. This is helpful if your file **only exists to get imported into a master style.scss and not explicitly compiled**.


For Example:

***_variable.scss*** 

	$primary: #000;

&nbsp;	
***_header.scss***

	header {
		color:$primary;
	}

&nbsp;
***_footer.scss***

	footer {
		background:$primary;
	}

&nbsp;
***custom.scss***:

	@import "_variable.scss";
	@import "_header.scss";
	@import "_footer.scss";

&nbsp;
***custom.css***

	header {
	  color: #000; 
	}

	footer {
	  background: #000; 
	}

&nbsp;


## Extends

In Sass, the **@extend** directive is an outstanding way to **inherit** already existing styles.

***extends.scss***

	.input {
	  border-radius: 3px;
	  border: 4px solid #ddd;
	  color: #555;
	  font-size: 17px;
	  padding: 10px 20px;
	  display: inline-block;
	  outline: 0;
	}

	.error-input {
	  @extend .input;
	  border:4px solid #e74c3c;
	}


***extends.css***

	.input, .error-input {
		border-radius: 3px;
		border: 4px solid #ddd;
		color: #555;
		font-size: 17px;
		padding: 10px 20px;
		display: inline-block;
		outline: 0; 
	}

	.error-input {
		border: 4px solid #e74c3c; 
	}


## Placeholders

The **@extend** directive allows us to easily **share** styles between selectors. This is best illustrated with an example:  

***.scss***

	.icon {
	  transition: background-color ease .2s;
	  margin: 0 .5em;
	}

	.error-icon {
	  @extend .icon;
	  /* error specific styles... */
	}

	.info-icon {
	  @extend .icon;
	  /* info specific styles... */
	}


***.css*** (generated css file)
	
	.icon, .error-icon, .info-icon {
	  transition: background-color ease .2s;
	  margin: 0 .5em;
	}

	.error-icon {
	  /* error specific styles... */
	}

	.info-icon {
	  /* info specific styles... */
	}	


Now here comes the interesting part. What if we **never use the icon class** in our markup and its **only purpose is to be there to extend**?  

The resulting CSS will be **slightly larger** than it really needs to be because we'll have a style that **will never be used**. We can get around this with **placeholder selectors**.


### Placeholder selectors

They are very **similar to class selectors**, but instead of using a period (.) at the start, the **percent character (%)** is used.  

##### Placeholder selectors have the additional property that they will not show up in the generated CSS, only the selectors that extend them will be included in the output. 


***.scss***

	%icon {
	  transition: background-color ease .2s;
	  margin: 0 .5em;
	}

	.error-icon {
	  @extend %icon;
	  /* error specific styles... */
	}

	.info-icon {
	  @extend %icon;
	  /* info specific styles... */
	}


***.css*** (generated css file)

	.error-icon, .info-icon {
	  transition: background-color ease .2s;
	  margin: 0 .5em;
	}

	.error-icon {
	  /* error specific styles... */
	}

	.info-icon {
	  /* info specific styles... */
	}


## Mixins

Without question, one of the most powerful and valuable features of Sass is the **ability to package up existing code into reusable chunks of code** called ***mixins***.


### Mixins are like Macros

Mixins are the Sass **equivalent of macros** in other programming languages.  
If you've programmed before you could think of them as **functions, procedures, or methods**, but they aren't technically any of these concepts because their function is to **generate code at compile time not execute code at run time**.  

&nbsp;
**The macros are the ones which generate code at compile time!**


This was all for theory. Let's now switch to code!

### Implementation 

We'll now write a **border-radius mixin** and use it in our code. Follow along!  

***.scss***

	@mixin border-radius($radius) {
	  -moz-border-radius: $radius;
	  -webkit-border-radius: $radius;
	  -ms-border-radius: $radius;
	  border-radius: $radius;
	}

***.css***

	a.button {
	  background: black;
	  color: white;
	  padding: 10px 20px;
	  @include border-radius(5px);
	}

	/*
	generated output

	a.button {
	  background: black;
	  color: white;
	  padding: 10px 20px;
	  -moz-border-radius: 5px;
	  -webkit-border-radius: 5px;
	  -ms-border-radius: 5px;
	  -o-border-radius: 5px;
	  -khtml-border-radius: 5px;
	  border-radius: 5px;
	}
	
	*/	


### Explaining the implementation
<ul>
<li>The declaration begins with the directive @mixin and is followed by the name of the mixin. In this case border-radius. </li> 

<li>The name of the mixin can contain any combination of alpha and numeric characters without spaces. </li> 

<li>Then comes the list of arguments that the mixin accepts enclosed in parentheses ( ... ). </li> 

<li>Next comes the definition of the mixin enclosed in braces { ... }. The definition of the mixin can contain any combination of CSS attributes. You can even declare additional rules (with selectors) that will be mixed into your CSS along with the attributes. </li>   

<li>Lastly, the mixins are used with the @include directive followed by the name of the mixin with respective arguments. In this case that was @include border-radius(5px). </li> 

</ul>

### Compass-Project Intro
This example lets us use **border-radius across all browsers**. There is a **project dedicated** to providing mixins just like that and much more. The name of the project is: **[Compass-Project](http://compass-style.org/)** and it is thought of as the **standard library for Sass**. 

### Default arguments

You can also add **default values to the arguments** that you pass into your mixin.  

***.scss***

	@mixin border-radius($radius: 5px) {
	  ...
	}

This makes the $radius argument **optional**. So you can call the mixin without it like this:	

	@include border-radius;

Which would use the **default value i.e. 5px** for $radius.


Another way to provide a default value is to **declare a variable** beforehand and **use that** as the default value for the mixin:  

	$default-border-radius: 5px !default;
	@mixin border-radius($radius: $default-border-radius) {
	 ...
	}	

## Keyword arguments

Keyword arguments are especially useful when a mixin accepts **multiple arguments**. If the arguments are defaulted, you can **use the name** of the argument to set the **specific value** for an argument, **without passing** the values of the other arguments. 

	@mixin border-radius($radius: 5px, $moz: true, $webkit: true, $ms: true) {
		@if $moz    { -moz-border-radius:    $radius; }
		@if $webkit { -webkit-border-radius: $radius; }
		@if $ms     { -ms-border-radius:     $radius; }
		border-radius: $radius;
	}

Since all of the arguments have default values, you could **turn off support for just Internet Explorer** by calling the mixin like this:


	@include border-radius($ms: false);

This is much **simpler than calling** the mixin with each of the arguments without names:

	@include border-radius(5px, true, true, true);

With keyword arguments, you **don't even have to call out to the mixin with the arguments in the same order that they were declared**: 

	@include border-radius($ms: false, $radius: 10px);	
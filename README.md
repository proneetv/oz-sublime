# Sublime Plugin for Oz (Mozart)
================================

Features
---------
* Syntax Highlight
* Autocompletion
* Build and Run from Sublime Text

Installation
------------
This installation procedures ensures automatic upgrades from the github repo.

* Press Ctrl+Shift+P and select Add repository 

![Package Control: Add Repository](http://www.macdrifter.com/uploads/2012/08/Screen%20Shot%2020120801_222551.jpg)

* Paste the repository url: https://github.com/2020saurav/oz-sublime

* Press Ctrl+Shift+P and choose Install Packages. The repository should be added as package "oz-sublime"

* In case you don't have Package Control, get it from https://packagecontrol.io/installation

Alternate Installation
----------------------
1. Clone the repository or download ZIP and extract to Oz directory
`git clone https://github.com/2020saurav/oz-sublime Oz`

2. Move this directory to Sublime package config
`mv /path/to/Oz/ ~/.config/sublime-text-3/Packages/`

Usage
-----
Use Ctrl+B to build and Ctrl+Shift+B to build & run

Sample Codes
------------
* Hello World

```oz
functor
import
	Browser(browse:Browse)
	System(showInfo:Print)

define
	{Browse 42}
	{Print "Hello World in console"}
end
```

* Scope, function, thread

```oz
functor
import
	System(showInfo:Print)

define
	local Factorial in
		fun {Factorial N}
			if N==0 then 1 else N*{Factorial N-1} end
		end
		{Print {Factorial 5}}
	end
	local Test in
		Test = 42
		{Print Test}
	end
	fun {Fib X}
		case X
		of 0 then 1
		[] 1 then 1
		else thread {Fib X-1} end + {Fib X-2} end
	end
	{Print {Fib 10}}
end
```

* Tail Recursion

```oz
 functor
import
	System(showInfo:Print)
define
	fun {Factorial N}
		fun {FactorialAux N Product}
			if N==0
			then Product
			else {FactorialAux N-1 N*Product}
			end
		end
	in 
		{FactorialAux N 1}
	end
	{Print {Factorial 5}}
end
```

WARNING
-------
Closing the browser window does not send a `SIGINT` interrupt signal, so the process `ozwish` and `ozemulator` lives unless explicitly killed. Browser opened from command line can be killed by sending `SIGINT` by Ctrl+C. 
To make it easy, one may keep alias in .bashrc:
```shell
alias ozkill='kill -9 `pidof ozemulator` && kill -9 `pidof ozwish`'
```


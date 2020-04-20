# ptkcmd

[View API documentation](http://htmlpreview.github.io/?https://github.com/mmiguel6288code/ptkcmd/blob/master/docs/ptkcmd/index.html)

ptkcmd adapts the built-in cmd.py standard library module to use prompt-toolkit instead of readline

```
from ptkcmd import PtkCmd, Completion

class MyCmd(PtkCmd):
    def __init__(self,stdin=None,stdout=None,intro=None,interactive=True,do_complete_cmd=True,default_shell=False,**psession_kwargs):
    	"""
	    stdin, stdout, intro are as defined in the standard library cmd.py

	    If interactive is True, then the prompt-toolkit prompt() method will be utilized from a PromptSession.
	    If interactive is False, then the prompt will be written to stdout and a line read from stdin

	    If do_complete_cmd is True, then completion will be performed for the initial command of each line against the list of known commands.
	    If do_complete_cmd is False, no completion will be attempted for the initial command.
	    In either case, completion can be attempted for the arguments according to any 'complete_' methods defined.

	    If default_shell is False, then receiving a command that does not have a "do_" method will result in writing an error to self.stdout.
	    If default_shell is True, then the command will be used as an input to subprocess.run(). The shell input to run() will be False.

	    If additional keyword arguments are provided, they will be passed to the PromptSession constructor that is used for prompts.
	    The only PromptSession keyword argument not allowed is 'completer'.

	"""
    	super().__init__(stdin,stdout,intro,interactive,do_complete_cmd,default_shell,**psession_kwargs)

    def do_mycmd(self,args)
    	"""
	This is a command named 'mycmd'.
	When a command is executed by PtkCmd, the initial line that is entered is split by shlex.split().
	The first item, i.e. the command, is used to determine which "do_" method to call.
	The args input is the list, excluding the command itself.
	All commands will show up when the help command is invoked.

	Typing 'help mycmd' will show the docstring of do_mycmd().

	"""
	...
    def help_mytopic(self):
    	"""
	This is a help topic named 'mytopic'.
	All topics declared in this way will show up when the help command is invoked.

	Typing 'help mytopic' will execute the help function, which typically will write some text to self.stdout
	"""
	...
    def complete_mycmd(self,args,document,complete_event):
    	"""
	This method defines completion rules for the command named 'mycmd'

	args = the entered line parsed by shlex, excluding the name of the command itself
	document and complete_event are as defined in the prompt-toolkit documentation
	Should yield Completion objects as defined in prompt-toolkit
	"""
	
```

# Cursor demo
- Start recording
## What
https://cursor.com
"Drop in" replacement for vscode, with more powerfull AI features for
writing and understanding code.
Indexes your code base.

## Why do I use Cursor?
- Makes programming faster and more fun
- I think LLMs will keep getting better at automating programming, and that the skill
of knowing how to use them well will become more valuable over time.

Note: I haven't used copilot in ~6 months. It might be way closer to feature parity with
copilot by now.
## Setup
- Guide https://neconcoimmunity.atlassian.net/wiki/spaces/OP/pages/1870004225/Cursor+AI+code+editor

- you are asked to import your setting and extensions from vscode
- remember to Enable privacy mode in the cursor settings

On mac it works very quite seamlessly. On ubuntu I had to set up the cli shortcut and
add the app to the app launcher manually. See guide for the details, I am also happy to
help.


## Example use cases
- Good at understanding a codebase
  - Indit: How are docker images run as prefect tasks in this codebase?
    - Clickable references
- Github code review like diff interface for applying edits
  - indit_flow.py: Add debug logs after each task
  - y/n to accept only parts
- Great tab complete
  - indit_flow.py rename logger to log
- Iterate on a failing test w cursor reading the test output
  - junction_scorer_test.py: I want to update the hotspot file parsing to raise on missing required columns. TDD
  - copy failing test output, use for implementation

## How I work
1. Starting a task often means starting a new thread in cursor
2. As much as possible give cursor the same context you have for completing the task
3. Cursor can help you plan the change to get structure: Fex uv chat
4. Implement one piece at a time. Cursor can be too eager to give you a lot of code up front.

For cursor to give the best suggestions and answers I try to
give it all the context I would want to have like:
* Documentation for the library I use
* Manual or documentation for the package (fex indit user manual on confluence) @user-manual
* Issue description from jira: What is your high level goal in the context for making that change?
* Link to a tutorial I am following, cursor will index pasted url by default
* Picture of the style of plot I aim to make

## Tips and tricks
###  Ctrl + enter for most queries
I find cursor is quite good at figuring out what files to read.
I ask most questions with codebase context using `ctrl+enter` instead of just `enter`.

If I am doing a task I have done before where I know exactly what files
to use as an example I will point it to the files: Implement this like we do in @file_1.py and 
write a test like in @test_file_1.py

Sometimes I constrain the context by pointing it to a folder @folder-name and submitting
with `enter`.

### Model selector
I recommend you use `claude-sonnet-3.5`.
o1-preview might be good for some algorithm or more heavy thinking tasks, but I don't know.
Let me know if you try o1-preview and find it valuable.

### Setting rules for cursors
- In your cursor settings
- Or repo specific with a .cursorrules file. 
  - Fex "never add print statements use a logger. Default to adding a logger.debug at any branch in the code"

```.cursorrules
When running python commands like pytest, you should prefix the command with 
uv run --extra dev. That ensure the python environment is active and up to
date for every command. Fex to run pytest:
uv run --extra dev pytest

Always prefer polars over pandas for new functionality. For existing 
functionality you can continue using pandas.
```

### Generate cli commands
`Ctrl + K` in the cursor terminal allows you to describe what you want do do on the
command line with natural language and have the command generated.

```shell
install ifconfig
rename the csv files to .tsv in this folder and it's sub folders
```

### Inject docs in your queries
You can inject up to date documentation from a library you're using by adding
@docs and selecting the relevant package
But sometimes cursor won't have the docs for your package, or the wrong version.
If all you need is a single page you can just paste the url to that docs page in
your query.
In the cursor settings you can add custom docs that are crawled and accessible
through @docs in any query you write.
Try https://docs.astral.sh/uv/ dask https://docs.dask.org/en/stable/
Later you can reference it with @my-custom-docs

Tip: Check that it actually indexed the library you wanted.

### Improving answer quality
LLMs are not deteministic. This means that sometimes just trying again can improve the answer.
Self reflection actually helps. If an answer looks fishy, I often ask `are you sure?`.

## Links
- Review of cursor with example videos (via Trym) https://www.arguingwithalgorithms.com/posts/cursor-review.html
- Cursor forums are very active and has many answers for cursor troubles or features https://forum.cursor.com/
- Cursor + zsh + python envs don't seem to work very well, you might have trouble running python commands through cursor. Ask me for workarounds. Bash works better. https://github.com/getcursor/cursor/issues/1484

## Extra
- point it to the readme or manual, say "help me set up and run this project"
- Include pictures of a plot you want to make: Try https://python-graph-gallery.com/circular-barplot-basic/ with a picture + run in notebook

### new module basde on junction scorer
Test composer?
We're implementing a new module for pre processing fasta files, we'll shift all the input amino acids by 1 in the input files for fun. The mdoule should be structured like @junction_scorer and I want workflo tests just like @test_junction_scorer.yaml . 

### Agent for solving a jira task
https://neconcoimmunity.atlassian.net/browse/ID-267
Copy title and description in score-epitopes. Run agent.

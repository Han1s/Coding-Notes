
you can accomplish a lot by just talking to it

## Notes
- www.claude.ai.design for design
	- you can drop in pictures in the cli as well
	- the output usually degrades in quality over time (maybe after 200-400k tokens)

- harness & model
- **models**:
	- **opus**
		- when the task needs deep reasoning and the answer is not just the code
		- problems with hidden causes that can be multiple layers
		- hard design choices
		- hard design choices
	- **sonnet**
		- when the answer to a task needs to understand the code
		- build a feature, fix a bug, refactor a module, add a test
		- understand what is happening
	- **haiku**
		- when a task has no real decisions, just steps to execute
			- mechanical work like find, list, reformat, rename, extract, summarize
			- following simple steps
- **effort model**
- the model is stateless
	- switching model midsession breaks cache
- **the harness provides the state**
- **assembled prompt**
	- **tool schema**
		- what the model can do (bash, edit, read, agent, etc)
	- **system prompt**
		- "you are claude code", environment, tone
	- **messages**
		- CLAUDE.md
		- available skills
		- message from the user

## Permissions, skills, hooks
- `/init` understands the code and creates .md file based on that
- the .md file usefulness depends on the models, the new models require it less.
- `/context`
- `/permissions`
	- you can specify what to allow, deny, ask, and default mode
- `/fewer-permissions-prompts`
	- detects which permissions youve been allowing all the time and suggest which to autoapprove
- description of the skills are really important

## Effort and Context windows
- `/advisor` - sets a different model for planning and for execution
- `/skill-creator` - to create and customize skills
	- almost always should use this probably
	- you can also use it to check whether the skill make the workflow better
- `/reload-plugins` - required if you added a new skill
- `/insights` - useful to see various inishgts
- `/powerup` - for onboarding to new users and workflows

## Hooks
- run custoom logic automatically at specific points of the lifecycle
- a specific event happens at a specific point
- `npx skills add xxx` you can add a skill from npm

## Subagents
- delete task-specific work to separate agents with their own context, tools, permissions
- `/agents`
	- displays the list of available agents, e.g. for planning, exploration, etc.
	- e.g. can create a **code reviewer**, etc.
	- subagents use a lot of tokens
	- subagents eventually go back to your conversation

## Agent Teams
- the main thread runs multiple agents that communicate with each other
- most of the time agent is probably enough
# Personal-LLM-prompts
A collection of the prompts and system prompts that I use for a couple of things. Below is a brief overview of each one:

### The system prompt
This is the base system prompt that I use with all LLMs; it establishes the LLM's behavior and personality. It is designed to set the tone and context for all interactions, tackling a couple of the most important general rules that the LLM should follow so that it consistently produces the best possible responses it's capable of. I keep iterating on it to refine its effectiveness.

### task-specific prompts
In addition to the system prompt, I maintain a small set of task-specific prompts tailored for different use cases I care about:
- learning-focused system prompt for coding agents
  - The way I use coding agents is a bit different from most people; I don't use coding agents to get answers or write for me. I use them as a thinking partner that's been explicitly instructed to push back, adapt to my actual understanding, and never sacrifice truth for comfort.
- Master CV creation prompt
  - designed to create me a master CV from a messy, unstructured input.
- job-fit assessment and resume tailoring prompt
  - designed to analyze job descriptions against my actual abilities as listed in the master CV and IF I am a good fit, create a tailored resume.
- LinkedIn profile evaluation prompt
  - designed to analyze my LinkedIn profile against meaningful criteria and provide actionable feedback for improvement.
- 'continuation system' prompt
  - This is a 2-part prompt, designed to let you continue your conversation in a new chat.

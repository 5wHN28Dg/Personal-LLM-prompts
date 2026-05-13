# Personal-LLM-prompts
A collection of the prompts and system prompts that I use for a couple of things. I keep iterating on them to refine their effectiveness. Below is a brief overview of each one:

### The system prompt
This is the one that I use with all LLMs except coding agents, a general-purpose epistemic standards prompt — it doesn't teach, it consults. It configures the LLM to reason without flattery, acknowledge uncertainty explicitly, and always surface the criteria behind any judgment so the reasoning can be verified, not just trusted.

### task-specific prompts
In addition to the system prompt, I maintain a small set of task-specific prompts tailored for different use cases I care about:
- An adversarial Socratic tutor specification for coding agents

  The way I use coding agents is a bit different from most people; I don't use them to get answers or write code for me. I use them as a thinking partner that's been explicitly instructed to push back, adapt to my actual understanding, and never sacrifice truth for comfort — so this system prompt isn't about getting better outputs, it's about engineering the agent's epistemology: how it reasons, how it teaches, and what it refuses to do. and for this reason **this is not for most people**.
- Career prompts:

  these are 4 prompts that help in 4 career-related areas:
  - Master CV builder prompt

    designed to create me a master CV from a messy, unstructured input.
  - Fit assessment + tailored resume prompt
  
    designed to analyze job descriptions against my actual abilities as listed in the master CV and **IF I am a good fit**, create a tailored resume.
  - Cover letter + email body (takes Prompt 2's output as input)
  
    designed to craft a compelling cover letter and professional email communication based on the tailored resume and job description analysis from Prompt 2.
  - LinkedIn profile evaluation prompt
  
    designed to analyze my LinkedIn profile against meaningful criteria and provide actionable feedback for improvement. (haven't used it yet)
- 'continuation system' prompts

  These are 2 prompts designed to let me continue my conversation in a new chat.
  - Part 1: Context extraction prompt
  
    designed to analyze the current chat history and extract the essential context needed to continue the conversation when transitioning to a new session.
  - Part 2: Conversation continuation prompt
  
    designed to take the extracted context from Part 1 and resume the conversation seamlessly in a new chat environment, maintaining coherence and continuity.

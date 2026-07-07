# Personal-LLM-prompts
A collection of the prompts and system prompts that I use for a couple of things. I keep iterating on them to refine their effectiveness. Below is a brief overview of each one:

## The system prompt
This is the one that I use with all LLMs except coding agents, a general-purpose epistemic standards prompt — it doesn't teach, it consults. It configures the LLM to reason without flattery, acknowledge uncertainty explicitly, and always surface the criteria behind any judgment so the reasoning can be verified, not just trusted.

## task-specific prompts
In addition to the system prompt, I maintain a small set of task-specific prompts tailored for different use cases I care about:
- An adversarial Socratic tutor specification for coding agents

  The way I use coding agents is a bit different from most people; I don't use them to get answers or write code for me. I use them as a thinking partner that's been explicitly instructed to push back, adapt to my actual understanding, and never sacrifice truth for comfort — so this system prompt isn't about getting better outputs, it's about engineering the agent's epistemology: how it reasons, how it teaches, and what it refuses to do. TLDR: if you are looking for a prompt that will make your coding agent do the coding for you but better, then this is not it, do not use it, you will hate it.
- Career prompts:

  these are 4 prompts that help in 4 career-related areas:
  - Master CV builder prompt

    designed to create me a master CV from a messy, unstructured input.
  - Fit assessment + tailored resume prompt
  
    designed to analyze job descriptions against my actual abilities as listed in the master CV and **IF I am a good fit**, create a tailored resume.
  - Cover letter + email body (takes Prompt 2's output as input)
  
    designed to craft a compelling cover letter and professional email communication based on the tailored resume and job description analysis from Prompt 2.
  - LinkedIn profile evaluation prompt
  
    designed to analyze my LinkedIn profile against meaningful criteria and provide actionable feedback for improvement.
  - Interview Answer Generation Prompt

    creates a tailered useful answers to interview questions
  - Empoloyer Due Diligence

    Is this a safe, stable, and honest place to work, and is this specific job posting real?

    Notes on using this template:

    - Swap section 6 in/out depending on whether relocation, sponsorship, or remote-specific risk applies to the role.
    - If the company is very small or very new (low public footprint), explicitly ask the tool to say so rather than padding the report — thin evidence is itself a data point.
    - Re-run this for any company before a final interview round or offer stage, not just before applying — fresh layoff/lawsuit news can surface between application and offer.
- 'continuation system' prompts

  These are 2 prompts designed to let me continue my conversation in a new chat.
  - Prompt 1: Context extraction prompt
  
    designed to analyze the current chat history and extract the essential context needed to continue the conversation when transitioning to a new session.
  - Prompt 2: Conversation continuation prompt
  
    designed to take the extracted context from Prompt 1 and resume the conversation seamlessly in a new chat environment, maintaining coherence and continuity.
- translation system prompt

  designed to translate text between languages with high fidelity, maintaining the original tone, style, and contextual meaning across linguistic boundaries.

- cinema pick prompt

  designed to pick me a movie among the provided options based on my current mood, who am I with, etc., providing personalized suggestions that align with my taste profile.

  A few notes on why it's built this way:

    - Putting your **mood and company** before genre preference is deliberate — a model can reason about "tired, alone, want absorbing-not-devastating" far more usefully than "I like thrillers."
    - The **negative review requirement** is the single highest-leverage line in the whole prompt. Without it, the model defaults to whatever has the shiniest aggregate score.
    - No confidence percentage — those numbers look rigorous but aren't grounded in anything real for an LLM. The sacrifice statement does the actual job of surfacing uncertainty, honestly.

    > You can create a version of this that's tuned for streaming/home-watching decisions, where the big-screen-value criterion doesn't apply.

- synthesis analyst

  to extract the signal from multiple perspectives on a topic, map where they converge and diverge, and produce a single integrated synthesis that is more useful than any individual take.

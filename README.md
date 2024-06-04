# Applied LLMs - What Weve Learned from A Year of Building with LLMs

https://applied-llms.org/

---

## Tactical: Nuts & bolts of working with LLMs

### Prompting

#### Focus on getting the most out of fundamental prompting techniques

- fundamental prompting techniques
	- A few prompting techniques have consistently helped with improving performance across a variety of models and tasks:
		- n-shot prompts + in-context learning
		- chain-of-thought
		- and providing relevant resources
- in-context learning via n-shot prompts (aka n-shot prompts + in-context learning)
	- is to provide the LLM with
		- **a few examples that demonstrate the task** and
		- **align outputs to our expectations**
	- If n is too low, the model may over-anchor on those specific examples, hurting its ability to generalize.
		- **As a rule of thumb, aim for n ≥ 5**
		- Don’t be afraid to go as high as a few dozen.
	- Examples should be representative of the expected input distribution.
		- If you’re building a movie summarizer, include samples from different genres in roughly the same proportion you’d expect to see in practice.
		-  You don’t necessarily need to provide the full input-output pairs. In many cases, examples of desired outputs are sufficient.
		-  If using an LLM which supports tool use, your n-shot examples should also use the tools you want the agent to use.
	- NOTE:
		- in-context learning means having information from within your prompt that helps the model learn.
		- n-shot means you put N times of example to give the context of how you want your output to be, to the model.
- In Chain-of-Thought (CoT) prompting, we encourage the LLM to explain its thought process before returning the final answer.
	- helpful to make the CoT more specific, where adding specificity via an extra sentence or two often reduces hallucination rates significantly.
		- For example, when asking an LLM to summarize a meeting transcript, we can be explicit about the steps, such as:
			- First, list out the key decisions, follow-up items, and associated owners in a sketchpad.
			- Then, check that the details in the sketchpad are factually consistent with the transcript.
			- Finally, synthesize the key points into a concise summary.
- Providing relevant resources
	-  a powerful mechanism to
		- expand the model’s knowledge base,
		- reduce hallucinations, and
		- increase the user’s trust.
	- Often accomplished via Retrieval Augmented Generation (RAG)
		- providing the model with snippets of text that it can directly utilize in its response is an **essential technique**
	- When providing the relevant resources, it’s not enough to merely include them;
		- don’t forget to tell the model to
			- prioritize their use,
			- refer to them directly, and
			- sometimes to mention when none of the resources are sufficient.
			- These help “ground” agent responses to a corpus of resources.

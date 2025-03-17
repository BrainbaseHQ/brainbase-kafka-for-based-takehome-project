# Brainbase – Vibe-code Agents
Brainbase is a powerful tool for provisioning complex AI agents. Even though our language can be written by humans, it was actually built to be written by AI, so that anyone, technical or non-technical can create their own agent just by talking.

We call it *vibe-coding your agents*.

We want you to build an early version of our next flagship product: Kafka

## Specifications
Kafka is our version of Cursor/Windsurf for vibe coding AI agents, which works very similarly.

1. The user starts off by describing their idea
2. Kafka creates a `.based` file based on the request
3. The user describes changes and modifications to the agent
4. Kafka creates changes in the form of code diffs and applies them when the user accepts
5. Kafka verifies the written code using the Brainbase based verification endpoint, and iterates on errors until resolved or hit maximum number of iterations (5 is a good number but up to you)

## Stack

Kafka has a frontend (client) and a backend (AI server).

Frontend: NextJS, React, Typescript, Tailwind CSS, Shadcn
Backend: Python

### Frontend
Kafka's frontend should look similar to Cursor/Windsurf and should be styled similarly to the following, internal version we have of Kafka:

<img width="1512" alt="image" src="https://github.com/user-attachments/assets/d8c13d2e-3147-4ded-b9cf-924f50673a8f" />

You are encouraged to use any frontend framework to copy this UI such as Bolt.new or Lovable.

### Backend
Kafka's backend needs to be written in Python and must be stateful (websocket connection). Here, there are no constraints on the agent framework underneath, however we've seen the best working ones to be just using pure LLMs that are provided necessary context and output diffs.

We suggest using unified diff format and applying changes using https://gist.github.com/noporpoise/16e731849eb1231e86d78f9dfeca3abc.

## Milestones
We expect you to approach this task in steps which have associated milestones:

### Milestone 1: Agent that can generate Based code and iterate
Create an agent that will take resources provided (including `BASED_GUIDE.md`) and be able to write simple Based code as output (not diff). Every time the agent writes a piece of Based code it should be run through the validation endpoint, if successful there are no further iterations, if failed the errors from the validation endpoint should be fed back into the LLM until it generates succesful code.

Exit criteria for milestone: Agent can write simple Based code and can iterate to fix errors

### Milestone 2: Agent that can generate Based diffs and apply
Modify your first agent to output not full Based code but unified diffs on the code written so far and then apply them. Should still be able to iterate. When the diff format is wrong, there should be a checker that notices the diff format is wrong and has the LLM redo it.

Exit criteria for milestone: Agent can write Based code diffs to modify the existing code and can iterate to fix errors

### Milestone 3: Websocket agent
The agent from Milestone 2 can be connected via websocket. In each websocket session, keep the messages so far in the websocket session in an array (you can also keep the code so far here), instead of relying on the client to keep passing in past messages in it's API requests.

Exit criteria for milestone: Agent can now run on a websocket

### Final Milestone: Client that can connect to this websocket
The client should be able to connect to the websocket agent from Milestone 3 and send messages. These messages should be handled in the backend server, and then the results should be returned.

Exit criteria for milestone: Client that can interact with the agent over websocket

## Rules and Guidelines
- Using coding assistants such as ChatGPT, Claude, Cursor and other are absolutely allowed and strongly encouraged. If you can build this entire project through vibe coding we have no problem with it :)
– Getting 3/4 milestones completely is better than getting 75% on all four milestones. Please follow the progression of the flows.
– Keep your code clean so we can go through it. We know code hygiene is hard to maintain when you're shipping fast, but it's important that we understand what you did. You can use Cursor before each commit to automatically go and comment out your code.
– For the purposes of this project, any Based code that passes the verification endpoint is considered correct Based code. This is not the case in real life as there can be logic issues but for this project you can assume anything that passes is correct.



# Bedrock + Wing Workshop  

_Building a Serverless Workflow, Powered by AI_

This repo is a step-by-step guide for an online workshop ([Eventbrite](https://www.eventbrite.com/e/amazon-bedrock-winglang-tickets-769562721817)).

## Any Issues? Questions? Let's Talk!  

Please [join Winglang's Slack](https://t.winglang.io/slack); we have a dedicated channel for this workshop [#workshop-bedrock](https://winglang.slack.com/archives/C06BWT4PC30).

## During the Session, You'll Learn the Following:  

- Intro to [Amazon Bedrock](https://aws.amazon.com/bedrock/)
- Use Amazon Bedrock Resources from Wing  
- Create a GitHub App
- Commit Code into Open PR
- How to Produce Ready-to-Apply Terraform Assets  

### Some General Resources:  

- [Learn about Inflights](https://www.winglang.io/docs/concepts/inflights) - Preflight and Inflight are Winglang's Most Important Core Concepts  
- [Cheat Sheet](./cheatsheet.md) - Let's Learn Wing in 5 Minutes, Shall We?
- [Language Reference](https://www.winglang.io/docs/language-reference) - A Complete Language Reference for Winglang  
- [Winglibs](https://github.com/winglang/winglibs) - Wing Trusted Library Ecosystem
- [Playground](https://www.winglang.io/play/) - Write and Test Wing Code Online  

## The Application  

A GitHub Application that Listens to Any Incoming Pull Requests and Corrects Spelling, Grammar & Punctuation for Any `*.md` Files that Were Changed during this Pull Request.  

### Workshop Sessions  

1. **Setup & Prerequisites** - Tools, Setup and Getting Access to AWS Bedrock Foundation Models ([link](./01-setup.md))  
2. **Why Winglang** - Short Recap](https://raw.githubusercontent.com/ekeren/react-wing-workshop/main/assets/why.pdf) - Problems with Serverless, and the Wing Approach  
3. **Introduction to Bedrock** - A Short Introduction to Amazon Bedrock Service by [Arik Porat](https://www.linkedin.com/in/arik-porat-15419426/), Solutions Architect at AWS  
4. Using Bedrock in Wing - Installing & Using `winglibs/bedrock` Module ([link](./04-bedrock.md))  
5. GitHub App DYI - How to Build Your Own GitHub Bot ([link](./05-github-diy.md))  
6. Wing's GitHub Module - Using `winglibs/github` Instead to Make an Uppercase Bot ([link](./06-github-winglibs.md)) 
7. Spell Checking with Bedrock - Modifying the Files Based on `winglibs/bedrock` ([link]((./07-wrap.md)))  
8. Thank You for Flying with Us - Deploy Application to AWS ([link]((./08-deploy.md)))  

---  

### What's Next?   

In the Next Session We Will Be Using [LangChain](https://www.langchain.com/) with [AWS Bedrock](https://aws.amazon.com/bedrock/) to Embed Documents into [Momento Vector Index](https://docs.momentohq.com/vector-index)


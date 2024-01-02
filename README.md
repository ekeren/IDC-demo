

# bedrock + wing workshop  

_building a serverless workflow, powered by ai_

this repo is a step-by-step guide for an online workshop ([eventbrite](https://www.eventbrite.com/e/amazon-bedrock-winglang-tickets-769562721817)).

## any issues? questions? let's talk!  

please [join winglang's slack](https://t.winglang.io/slack); we have a dedicated channel for this workshop [#workshop-bedrock](https://winglang.slack.com/archives/c06bwt4pc30).

## during the session, you'll learn the following:

- introduction to [amazon bedrock](https://aws.amazon.com/bedrock/)  
- use amazon bedrock resource from wing
- create a github app
- commit code into open pr  
- how to produce ready-to-apply terraform assets  

### some general resources:  

- [learn about inflights](https://www.winglang.io/docs/concepts/inflights) - preflight and inflight are winglang's most important core concepts.
- [cheat sheet](./cheatsheet.md) - let's learn wing in 5 minutes, shall we?  
- [language reference](https://www.winglang.io/docs/language-reference) - a complete language reference for winglang.  
- [winglibs](https://github.com/winglang/winglibs) - wing trusted library ecosystem  
- [playground](https://www.winglang.io/play/) - write and test wing code online.   

## the application   

a github application that listens to any incoming pull requests and corrects spelling, grammar, and punctuation for any `*.md` files that were changed during this pull request.   

### workshop sessions   

1. **setup & prerequisites** - tools, setup and getting access to aws bedrock foundation models ([link](./01-setup.md))  
2. **why winglang** - short recap](https://raw.githubusercontent.com/ekeren/react-wing-workshop/main/assets/why.pdf) - problems with serverless, and the wing approach.    
3. **introduction to bedrock** - a short introduction to amazon bedrock service by [arik porat](https://www.linkedin.com/in/arik-porat-15419426/), solutions architect at aws.  
4. using bedrock in wing - installing & using `winglibs/bedrock` module ([link](./04-bedrock.md)).
5. github app diy - how to build your own github bot ([link](./05-github-diy.md))  
6. wing's github module - using `winglibs/github` instead to make an uppercase bot ([link](./06-github-winglibs.md)).  
7. spell checking with bedrock - modifying the files based on `winglibs/bedrock` ([link](./07-wrap.md))   
8. thank you for flying with us - deploy application to aws ([link](./08-deploy.md))  

---

### what's next?   

in the next session, we will be using [langchain](https://www.langchain.com/) with [aws bedrock](https://aws.amazon.com/bedrock/) to embed documents into [momento vector index](https://docs.momentohq.com/vector-index).


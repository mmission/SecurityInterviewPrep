## About my experience at wday

### In this interview we'll look to assess your experience and exposure to Security related projects. You should be prepared to talk about the projects you've worked on in terms of the technical decisions you made or participated in, the way you collaborated with colleagues, and how the project fit into the bigger picture.

Key Attributes:

* Communication: Go beyond buzzwords, explain how your implementation worked in-depth and why. Your interviewer should understand and have a clear picture - share any assumptions made and the big picture, or other parts that affected your implementation. Lead the discussion and be engaging.

* Passion: Showing passion about your project. Why was it exciting, interesting, and challenging?

* Trade Offs: Be able to go over pros/cons for each decision (technologies used, architectural decision, creating your own solution vs open source). Be prepared to answer why you picked something.

* Technical Curiosity: Go beyond surface level to explain your research and understanding. Show your appreciation for technical details, and be able to go in deep on technical aspects. Expect to be asked specific questions about your implementation and thought process.

* Understanding Impact: Being able to go over the impact of your project, go over metrics for how you measured different parts, and what were the factors for success. How did it affect the business, the market, the product, and your users? What changed and what was the outcome?


## My answer

The big problem our App Sec team was re-formed to solve is to update our SAST and DAST solutions as a portion of our SDLC. For the past two years we have been working on revamping SAST we have faced some challenges and also made some great impact. The first piece we wanted to build was a REST API to inventory all of the codebases at Workday to have more knowledge about which developer teams owned which projects and how often those projects were being updated. This piece took longer than expected because the team, before I joined, decided to build the API in Scala in order to get more familiar with the language since they had been doing Scala specific AppSec reviews etc. Since the team went with a language that no one on the team besides the principal security architect was familiar with the learning curve was steep, which ultimately impacted the timeline of the project. We had budgeted that with our current review work and the project work it would take about 6 months to build out this API. [Another mistake that we made, which impacted our timeline was involving other security teams early on because they added extra functionality that we didn't include in our first design because we were trying to move quickly and jump to our next step of finding a new SAST solution.] With the API we can establish a webhook with Bitbucket/GHE and get notified of all open pull requests, merges to master, etc. From there we wanted to use our new SAST tool scan the changes that have been made to the repo and be able to comment back on open PRs or create new jira tickets for the appropriate dev team so that they can look at any potential vulnerability finding.  


maybe kinda confusing.. go back and refine later








The main concern was that the Application Security team didn't know which code bases at workday have been reviewed/how often they have rrevi...

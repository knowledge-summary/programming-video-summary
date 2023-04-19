# System Design Interview: A Step-By-Step Guide
*(link: https://youtu.be/i7twT3x5yv8)*

System design interview framework

Interview is stressful, and there is very little time to show off what we are capable of. A framework leads us to ask the right questions and focus on the right things.

Step:
1. Understand the problem and establish design scope (5 mins)
2. Propose high-level design and get buy-in (20 mins)
3. Design deep dive (15 mins)
4. Wrap up (5 mins)

First 5 mins - introduction

Middle 35-45 mins - The framework 

Last 5 mins - Q&A


## Step 1: Understand the problem and establish design scope
System design are usually
- open ended, presented in a way that is deliberately vague
- tests out ability to organize our thoughts and focus on what is important

It is our job to ask questions to understand the problem fully, before giving a solution.

The goal is to clarify the requirements
- Why we are building the system
- Who the users are
- What feature we need to build

Example: There can be many types of chat apps on the market

The final goal is to understand the features we are building in priority order. We should focus on the top few features to build and make sure that the interviewers agrees to the feature list.

It is also important to ask questions to clarify the non-functional requirements. They are what make the design unique and challenging.
- Security
- Consistency
- Freshness
- Accuracy
- Performance (more important)
- Scale (more important)

Example
1. Twitter clone with hundreds of users
2. Twitter clone with hundreds of millions of users with some popular account having millions of followers

The more senior the role, the more important to demonstrate our ability to handle the non-functional requirements.

To get the general sense of scale of the system and the potential challenges and bottlenecks, we might need to do some rough calculations. We want to get the order of the magnitude right.

End result: A short list of features to design for, along with a few important non-functional requirements to satisfy.


## Step 2: Propose high-level design and get buy-in
For most designs, 
- Top-down approach
- Start with the API design (establish the contract between the end users and the backend systems)
  - Follow RESTful convention unless specified otherwise
  - Define the input and output of the API
  - Verify that the API satisfy the function requirements
  - Example: Designs that requires two-way conversation between client and server -> Use WebSocket (con: as it is stateful, it is more challenging to scale)
- High level design diagram
  - Verify that the design satisfies all the feature requirements end-to-end
  - For many design, it starts with a load balancer or API Gateway
    - Behind that are the services that would satisfy the feature requirements (e.g. location-based service)
    - Data storage layer (usually not necessary to specify the exact database) (e.g. Google Maps client need to send frequent GPS updates to the server)
    - Repeat for all major features to complete the high-level design diagram

  > While developing the high-level design, maintain a list of discussion points for later (e.g. Database scaling, high concurrency, failure scenarios)

  > Resist the temptation to dig into too much detail too early before having a full picture of the design
  - Hash out the data model and schema (data access pattern, read/write ratio)
    - At scale, data model can significantly impact the performance of the design
    - Discuss the database to choose, and maybe the indexing option if it is simple
  - Review the high level design and make sure that each feature is end-to-end


## Step 3: Design deep dive
We can identify area that can potentialy be problematic and come up with a solutions and discuss trade-offs. In a typical interview, we should only have time to dive deeper into the top 2 or 3 issues.

We should work with the interviewer closely to decide what to discuss in depth.

This section is where non-functional requirements make the problem interesting. It is open-ended, and there is no one-size-fits-all approach.

Here is where the ability to 'read-the-room' is useful. Sometimes the interviewer's body language might give away clues that they are dissatified with certain aspects of the design. It is important to pick up these clues and make sure that the issues are addressed.

- Asking questions
- List out the reasons for choosing a particular solution (e.g. open source, handles a large volumes of writes, highly scalable)

Once we pick up problem to deep dive, we should come up with multiple solutions and discuss the trade-offs for each option.

Mini guidelines to frame the discussion
1. Clearly articulate the problem (e.g. Goole Maps have the write QPS at 1M/sec to the location database)
2. Come up with at least 2 solutions (e.g. reduce the location update frequency per user, choose a NoSQL database that could handle the write rate)
3. Discuss the trade-offs of the solutions (use numbers to back up our design)
4. Pick a solution and discuss it with the interviewer


## Step 4: Wrap up
Spending  a few minutes summarizing the design, focus on the parts that are unique to the particular situation. Keep it short and sweet.

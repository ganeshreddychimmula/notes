
2025-09-15 11:30

Status:

Tags: [[../../3 - Tags/DAS]]

---
# Reddit responses

## 1:

The biggest thing to keep in mind when flying solo is to have a little voice in your head saying "is there a way to roll back what I am doing if I screw it up?" Not unlike solo climbing you always need to keep in mind recovery and the control plane over everything else. You cannot get out of a tailspin without it.

- The tool needs to work for everyone in it.
- Look but don't cut! At least at first. Understand the biggest, most important integrations. Your most important tool is Miro. Figure out what it does, what the integration points really are.
- How well do you know Coda? What are the ==best practices==? How do people build in it? Knowing where you are going is perhaps more important than where you are coming from.
- The trickiest thing is cutover. The best way I have found to do it is to build the new tool as a strict, automated import from the old tool. That way you can repeatedly pull in the data to test things and you are never stuck in the "we started cutting over and something broke" gap.
- Make sure you think about maintenance when you are building. Your future self will thank you.
- That said, using some sort of tracking system to capture project planning and bugs makes a ton of sense. I would use coda for this as part of my familiarization process.

Documentation

- at this scale, documentation is another thing that can break. Make sure there is a clear runbook, but getting stuck document just adds more work and more things you need to maintain with little or no payoffs.
    
- that said, document landmines! Stuff that gets you in trouble, weird integrations. Your future self will thank you.
    
- always code like the guy coming behind you is a violent psychopath who knows where you live.
    
- at this scale, hand-off is going to be a meeting not a document drop.
Feedback

- I would lean into clickup first. Being able to have a simple mechanism -- like "email [app-feedbac@example.com](mailto:app-feedbac@example.com)" -- is very very handy. You can usually triage issues very easily, you don't get much data in most cases.
    
- You won't get much feedback.
    

Also, make sure to read Don't Make Me Think by Steven Krug, it will help you figure out the right UI things to do.

### Insights and Takeaways:
The core theme is **pragmatism over process**.
- Top priority is risk management. 
	- Since there is no backup, must always have a way to undo last action("roll back").. This "control plane" or recovery plan is more important than any new feature.
	- In tools like Airtable and Coda, a small change to a core table or an automation can have massive, cascading effects. Without a rollback plan, you could corrupt data or break a critical workflow with no easy way back.

- Getting started: Keep in mind, that tool need to work for everyone in the Org.
	- At this small scale, the system only needs to work for a few key people. Understanding their specific needs and the political landscape is more important than pure technical perfection
	- You're not just migrating a database; you're changing how people work. If you build a technically brilliant system that doesn't solve the right person's problem, the project will fail. Mapping it out first ensures you don't miss a critical, "weird" integration.
- Use Miro, to map out things.
	- using a tool like **Miro** to visually map out the current system, its integrations, and workflows _before_ I make any changes.
- Instead of a one-time, high-stress "cutover" from Airtable to Coda, he suggests building an **automated, repeatable import** from the old system to the new one.
	- This allows you to keep the old Airtable system running while you build and test in Coda. You can pull in fresh data every day to test your new Coda setup with real information without any risk. When you're finally ready to go live, the final "import" is just one last run of a process you've already perfected. This dramatically reduces the risk of the cutover process.
- Checkout best practices in Coda. 
- Checkout how others are building them.
- Don't try to document every single field and formula. That documentation will become outdated and a chore to maintain. Instead, focus on creating a "runbook" for essential processes and, most importantly, **document the "landmines"**—the weird integrations, the tricky parts, the things that could easily break.
	- "always code like the guy coming behind you is a violent psychopath who knows where you live," is a famous and humorous way of saying "write clear, simple, and maintainable code/solutions."
	- A future person doesn't need to know why you named a field `_v2_final`; they _do_ need to know that if they change it, the Google Calendar integration will break.
- Make giving feedback extremely simple (like a dedicated email address). Don't expect a lot of it. For building the user interface, he recommends the book _Don't Make Me Think_ by Steve Krug, which is a classic guide to making intuitive and user-friendly designs.

---

## 2

Firstly, you are not just a developer; you are a solution architect. Your goal is not to recreate Airtable in Coda. Your goal is to build a better system in Coda.

I'd stop thinking about "migration". Think about "rebuilding".

Sit with every single team that uses the current Airtable base. Watch them work. Don't just ask what they do, see the pain points, understand the workflow in and out.
-  What slows them down?
- What are their workarounds?
Everything needs to be documented
 I would be more keen on understanding what 20% that does 80%: You will find that maybe only 15-20 tables are used daily. Identify them. They are your Phase 1.

For a one-person team, full Agile/Scrum is overkill. we are a scrum team of 11, fine for us. But its principles are gold. Adapt them. May be break the project into small, 2-week phases. 

Phase 1: Migrate a few core tables and their main automation. A basic Excel or any basic backlog to track To Do, In Progress, Blocked, Testing, Done.

Mandate a daily stand up for yourself. Sounds stupid, I know. But always keep these 3 questions off top of your head What did I do yesterday? What will I do today? Any blockers? This self-accountability is key.

Documentation is non-negotiable, especially for your visa situation. Your documentation is your handover. Create a Project Bible. Like Business Requirements, Architecture diagram, data dictionary, Automations & integrations Log, User Manual?

Non-technical users will have endless ideas. You must manage them, not just implement them. Create a Request Portal where users can submit requests.

### Insights and takeaways
This response focuses heavily on process. The core theme of this response is **"Think Like a Product Manager, Not Just a Coder."**

- The goal is not to recreate Airtable in Coda. The goal is to build a better system in Coda.
	- Stop thinking it as "migration". Think about "rebuilding".
- The Discovery Process: The 80/20 Rule
	- Deeply understand how people _actually_ work by observing them. The key insight here is to apply the Pareto principle (80/20 rule): find the 20% of tables and workflows that provide 80% of the value. These become your priority for "Phase 1."
	- This is the antidote to feeling overwhelmed. You don't have to tackle all 40+ tables at once. This method gives you a clear, data-driven way to identify a manageable and high-impact starting point.
- **"Agile-Lite Approach"**: 
	- Full-blown agile/scrum process is an Overkill. However, Agile _principles_ like breaking work into small phases (sprints). 
	-  **Mandate a daily stand-up for yourself,** answering the three classic questions: 
		- What did I do yesterday? 
		- What will I do today? 
		- What are my blockers?
 - Documentation: The "Project Bible"
	 - The concept of a "Project Bible" includes specific artifacts: Business Requirements, Architecture Diagrams, a Data Dictionary.
- The "**Request Portal**"
	- Don't let user feedback and ideas become a chaotic stream of emails and messages. Create a formal, structured system (a "Request Portal") where users must submit their ideas.
	- First, it respects your time by batching feedback into one place. Second, it allows you to manage expectations. Just because an idea is submitted doesn't mean it will be implemented. It turns you from a reactive order-taker into a proactive manager of the product's scope.






---
## References
[Cutover](../../6%20-%20Main%20notes/Vocablury/Cutover.md)
[[Different Ways You Can Perform the Cutover ]]

2025-09-05 11:27

Status: #Comeback

Tags: [Best Practices](../3%20-%20Tags/Best%20Practices.md)

---
# Taking Ownership - Product Ownership

## The gist

- Focus on understanding the customer/end-user needs, not just completing the task
- By adopting a product-oriented mindset, engineers can ensure that even minor adjustments align with the overall product vision and deliver value.

**Cultivate a product focused mindset.**
- **Connect with the customer**. Get direct exposure to customer interactions and feedback, not just information filtered through a product manager. Participating in user research, reading customer support tickets, or engaging with users on a call can build empathy and illuminate the **`"why"`** behind your work.
- **Define and test assumptions**. For every small change, ask what problem it solves for the customer. Treat each feature as a hypothesis to be validated with real-world feedback. Don't be afraid to test your assumptions through low-effort methods like A/B testing or measuring key metrics to see if the change had the intended impact.
- **Understand the business context**. Grasp how your small change contributes to the larger product goals and business outcomes. Understanding the strategic purpose helps you make better decisions, prioritize effectively, and proactively identify opportunities for improvement

Take action on small changes

- **Think beyond the code**. See every task as a feature with a lifecycle, not just a line item on a to-do list. Consider not only the technical implementation but also the testing, documentation, and the long-term maintenance of the change.
- **Take initiative beyond your immediate task**. If you find a bug or spot a minor inconsistency while working on a feature, don't ignore it just because it's not in your assignment. A true owner is willing to take on small fixes and improvements that enhance the overall product quality.
- **Own the entire delivery process**. Push for your change to be successfully deployed and used by customers. This includes collaborating with QA, monitoring the release, and tracking its performance post-launch to ensure it truly solves the intended problem.

Communicate and collaborate effectively

- **Speak up in planning and refinement**. During sprint planning or backlog refinement sessions, don't be passive. Ask clarifying questions about the goal of a feature. Engage with product managers and designers to ensure a shared understanding and challenge assumptions constructively.
- **Provide valuable feedback**. Use retrospectives to share your perspective on how a feature rollout went. Did you uncover any issues during implementation? Did the customer feedback align with your expectations? This helps build a culture of continuous improvement.
- **Lead by example**. Show your teammates what ownership looks like. By consistently demonstrating curiosity, proactively addressing issues, and connecting your work to the customer, you'll encourage others to do the same.

---
## who owns what [^1]
There are several key areas of ownership needed to build successful products. Either Product or Engineering can own each, and the owner should take responsibility for getting their partner’s input and alignment on key decisions.

- 🧭 A simple set of principles to be clear on who owns what between Product and Engineering 
    - 🤔 **Why**? (Why build this?) - Owned by **Product**
    - 💡 **What**? (What are we building?) - Owned by **Product**
    - ⚙️ **How**? (How will we build it?) - Owned by **Engineering**
    - 👥 **Who**? (Who will build it?) - Owned by **Engineering**
    - ⏳ **When**? (When will it be ready?) - Owned by **Engineering**

### The Why?
Why are we working on this area? Why is this a problem worth solving? What change are we as a team hoping to produce in the world?

Answering this “Why?” question with conviction requires a strong understanding of our customers' wants (present and future), the market direction, the overall business strategy, and a deep understanding of the current product. 

### The what?
The “What?” relates to the specific features or products a team plans to release. What are we building to solve the problem we have pinpointed in the “Why”?

The “What?” goes beyond the basic functional requirements (we need to be HIPAA compliant) and into the specific requirements of a product to be ready for general availability (what specifically needs to happen for us to be HIPPA compliant). These details are critical to inform the key decisions Engineering must make, like “When?” “How?” and “Who?”. More on these below.

---
## How I Own Projects as a Software Engineer [^2]

When you take ownership of a project, something changes. You become responsible for everything that happens with the project.

Things go wrong? That’s on you. Customers are unhappy? That’s on you. You shipped something that doesn’t solve the problem? That’s on you.

### Gather context
- Understand problem - meaning understanding usecase
	- What problem does it solve?
	- Is it problem for everyone?
- People are having trouble discerning notes and the context of the video
- How others have solved this problem.
- How was this handled before.\
- Our goal should the end users shouldn't have trouble understanding - Put in users shoes

### Figure out a solution

Taking inspiration too heavily from existing solutions. How can you build a better version if you repeat the same mistakes they’ve made?

Another trap is thinking only in terms of what’s possible technically. This is specially a problem with engineers. You know how the system works, you know the compromises you’ve made, so you limit the world of possible solutions that fit into these existing constraints. This is a problem, because it often underestimates what’s possible.

Ask Yourself:
- What solution would completely solve this Issue? ( Even if it is not practical, disregarding technical constraints ) - Ideal solution
- What is about the ideal solution would be that makes it Ideal? What is the crux that solves the problem?

When technical constraints clash against the ideal, I can go back to the first principles. Now, given I want to preserve these principles, how can I solve this problem?

The above question forces me to think of levers I can pull. 
- We often believe that the only lever we have is the technical constraints: What clever optimisations can I do that will make this possible?
- But this isn’t true. There’s another powerful lever we have: solving the problem differently. In practice, this means changing the UX, while preserving the first principles.

### Build

As the owner, the biggest responsibility here is setting priorities. Priorities help everyone move quickly and get shit done. 
Great Read - [making things happen.](https://scottberkun.com/2012/how-to-make-things-happen/) 

This means creating an ordered list of tasks that need to get done to achieve your goals. For huge projects, I might use a Kanban board, but for smaller ones, a single GitHub issue seems ideal. For example, here’s one [I created for Experimentation](https://github.com/PostHog/posthog/issues/7462).

Try getting a MVP first: Choosing what parts are important needs the right priorities set. Does it need proper UIs or not? Can it work with mock data? What’s the smallest working expression of our first principles?

Get my priorities in order & follow through on them.  Whatever is the highest priority gets done first, no matter what comes in.

Ask Yourself, which do you fall under or which others fall under?
1. Do they ask for help if they get stuck.
2. To be productive, do they need me to (a) just set context; or (b) micromanage.
3. What are their strengths?
4. Are they gear-driven or behaviour-driven?
    
    I’m very gearsy - which means when I propose UX designs, I tend to go for “transparent internals” approach. As I’ve come to see, this is almost always the wrong thing to do. Most users don’t care about how their problems are solved, just that there’s a button which solves them.
    
5. ????

### Gather Feedback

 Nothing compares to the high fidelity one on one feedback, where you can go deep into whatever they say.
 
When gathering feedback, there’s two important things you’re testing:

1. Whether the principles you arrived at are indeed the first principles.

	It’s easy to misunderstand what users really want. With a concrete MVP in place, you could ask hypotheticals like: “How would you do `<Important Thing>` if this feature didn’t exist?”. You’re looking for confirmation that the information you gathered in the first step is still valid.


2. Whether your solution is a reasonable expression of those first principles.

	Don’t just confirm you’re on the right track; ensure you actually solve the problems.  For example, “Say you want to create a new experiment. How will you do it?”. I often follow up with questions, like ‘What do you think this graph means?’ or ‘Why are you getting that warning?’

 After these challenges, it’s a good idea to ask for general feedback: What’s missing? What do you love? Did this solve your problem?

At the end, you want to come out with two things: (1) Do users love this? and (2) If not, what’s missing? What do you need?

### Align metrics with feedback

Just having happy users in feedback calls isn’t enough. I always need to ensure that metrics line up with what users are saying.

I like to go through two cycles of `Gather context -> Figure out solution -> build -> gather feedback`. At this point, things are usually good to go. If I’m doing things right, the second cycle is much faster: it’s adding on functionality that we skipped in the MVP, so the gathering context & figuring out solutions steps can mostly be skipped.

 You ought to be able to answer questions like: “How many people are using it?”, “Of the people using it, how many find it valuable?”, and any other relevant product questions.

### Meta: Create feedback loops

 To work quickly & to make sure you’re doing the right things, you need several feedback loops. Both, long term and short term.

Each step above has its own quick feedback loops, where you get feedback within hours.

Do it with your teammates (specially product owners). Explore competitor products together. Make the thread open, so everyone in the company can see and contribute to it. It’s valuable to hear from colleagues who might have more context because they were an insider.

In the building phase, fast feedback loops mean small pull requests and quick reviews! Imagine how much faster you get things done and how much better your code looks when you have small PRs that get reviewed quickly, vs. a 500 line change that takes ages to get reviewed.

Apart from these quick feedback loops, there are slower but still important feedback loops between consecutive steps. The stage outputs aren’t set in stone. There’s going to be times when things come up that you didn’t think about earlier.

New technical constraints might show up while implementing the solution, that forces you to go back to the “figuring out the solution” stage. Don’t get married to the initial idea you came up with. Divorces are hard.

The longest feedback loops come with usage over time. This means tracking your metrics properly. The final step, “aligning metrics with feedback” is precisely this: a long feedback loop that gets rid of the noise and shows you exactly how users are using this product.

### Conclusion

I figured the hard part of software engineering was building things. But now, maybe it’s figuring out what to build. Knowing what to build seems rarer. That’s surprising to me, since you don’t need to know how to code to figure out what to build.


---
## References
[^1]:  https://www.jeremybrown.tech/product-and-engineering-who-owns-what/
[^2]: https://neilkakkar.com/How-I-Own-Projects-as-a-Software-Engineer.html
[How to work out what your users really need](../2%20-%20Source%20Material/Articles/How%20to%20work%20out%20what%20your%20users%20really%20need.md)
[How to Make Things Happen](../2%20-%20Source%20Material/Articles/How%20to%20Make%20Things%20Happen.md)

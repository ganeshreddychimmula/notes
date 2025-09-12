
2025-06-24 17:27

Status:

Tags:  [JavaScript](../../../3%20-%20Tags/JavaScript.md)

---
# Why React over Vanilla JS
### When to Opt for React?
>when a ==page changes frequently and drastically because of changes in either internal (state) or external (database, API, etc.) data.==  [^1] 

- At any point, your friends could tweet or like your tweet, and you want to see it right away. And you want to be able to shift from reading tweets to replying, liking, or tweeting at any moment without things slowing down or feeling disjointed.
- With vanilla JS, it would be quite messy and you need to manually consider lot of constantly updating, changing parts of application.
- Reusability with minimum instructions is a real plus in React.
- You can define and control the circumstances how and when you want to re-render DOM nodes

## Discussion from Reddit

> I assume that React is good for web apps that use a certain API. I'm usually building smaller multi-page projects that need some light interactivity and DOM manipulation, so I'm guessing that React would be an overkill in these types of situations?

You have the right instinct. As with most frameworks, you usually shouldn't use it until you find that your other tools are failing you somehow.

React (and Vue, etc.) is good, in my mind, when a ==page changes frequently and drastically because of changes in either internal (state) or external (database, API, etc.) data.==

A really good example is something like Twitter. At any point, your friends could tweet or like your tweet, and you want to see it right away. And you want to be able to shift from reading tweets to replying, liking, or tweeting at any moment without things slowing down or feeling disjointed.

To do all of that with vanilla is possible, but the code required to do so would be messy, likely less efficient than React, and probably quite fragile because of all the moving pieces you have to keep in mind.

The other really good use for React is code organization and re-use. If I'm making a Twitter clone, I want "like" buttons everywhere. Each tweet should have one. And they are all going to do the same exact thing, just with different data. With React, I just need to make one LikeButton component and drop it in wherever I want it.

You could use an **event bus library** to decouple components written in Vanilla JS. A set of components can be made to share a unique "event environment" (an environment where every component belonging to it can read other component's events within that environment).

Frameworks like React shine when you need to create and/or re-render DOM nodes. Your logic becomes really robust since you describe all possible ways something can be rendered right off the bat, instead of having to write and deal with every possible absurd combination "manually".

If all you really need is to toggle a modal and submit a form, React might indeed be overkill — at least initially.

 [javascript vs react: Choosing the right tool](https://www.asynclabs.co/blog/software-development/vanilla-javascript-vs-react-choosing-the-right-tool-for-web-development/)

React is particularly useful in scenarios where there is a ==lot of user interaction== on a web page, and it needs to respond quickly. It uses a ==Virtual DOM that tracks changes== on the web page and only updates the parts that require changes, making it efficient and fast. React provides excellent performance and ease of use for building complex web applications.

React has a vast ecosystem of extensions and plugins to help you create more robust and **scalable web applications**. Compared to Vanilla JS, it offers more advanced features, like server-side rendering, functional programming, and state management. React makes it easy to scale your application as it grows, and you can build scalable applications with a smaller team, making it cost-effective.

---
## References

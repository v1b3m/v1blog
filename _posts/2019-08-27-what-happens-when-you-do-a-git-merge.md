---
title: 'What happens when you merge a conflict on GitHub'
date: 2019-08-27
categories: [GitHub]
tags: [conflicts, merge]
---

If you've collaborated on GitHub then you've, at least once been in that situation where you have to resolve a conflict because a colleague pushed code to the same file as the one you wanted to push a commit to. Well, there's a number of ways to go around this, with the easiest being using the editor provided by GitHub online. Unfortunately, this editor can also do so much since for complicated conflicts, you'll have to merge the conflict locally on your repository and then push the changes to GitHub to resolve it. You'll most probably see something like this on your GitHub:

Well, enough with the explanations since that is not the reason I made this post. I actually made this post to talk about what happens in the background when you resolve a conflict. So, lets assume we have three branches `master, develop and ft-new-feature`, with branches `develop and ft-new-feature` created off of `master`.

```javascript
// index.js on master
const hey = (name) => {
  console.log(`Hello, ${name}`)
}
```
So, your work mate Leo edits file `index.js` on develop and makes changes to the exact section of code in the file as you've made in  `ft-new-feature`. So leo makes a pull request to master and merges that section of code to master. Shortly after, you make your pull request to master without knowing that Leo just made changes to `index.js`.

```javascript
// Leo's changes on develop
const hey = (name, age) => {
  console.log(`Hello, ${name}, congs on making ${age} years`)
}
```

```javascript
// Your changes after leo has merged his changes
const hey = (name, age) => {
  console.log(`Hello, ${name}, are you really ${age} years old`)
}
```

Then boom, a scary message just appears on your screen out of the blue.
```
X Can’t automatically merge. Don’t worry, you can still create the pull request.
```

A button with the words 'Merge Conflict' will be shown and it will lead you to a page with another button telling you to Resolve conflicts that will lead you to a page with an open editor:
```js
const hey = (name, age) => {
<<<<<<< ft-new-feature
  console.log(`Hello, ${name}, are you really ${age} years old`)
=======
  console.log(`Hello, ${name}, congs on making ${age} years`)
>>>>>>> master
}
```
Basically, what this page is telling you is to choose which code should be merged into your branch. Yes, you heard me right, **Your branch(ft-new-feature)**. To merge the conflict, you'll then have to edit out one of the versions of the code and also the conflict markers i.e
```
<<<<<<< ft-new-feature
=======
>>>>>>> master
```

So, after that long introduction, it's about time I get into why I wrote this article. What happens when you do a merge conflict?

So, I edited out the rest of the code and left index.js with the following contents:
```js
const hey = (name, age) => {
  console.log(`Hello, ${name}, are you really ${age} years old`)
}
```
I then, marked the file as resolved and then commited the merge. At this time, if you check master, index.js will contain the following code:
```js
const hey = (name, age) => {
  console.log(`Hello, ${name}, congs on making ${age} years`)
}
```

And, on checking ft-new-feature, we get:
```js
const hey = (name, age) => {
  console.log(`Hello, ${name}, are you really ${age} years old`)
}
```

To be continued...

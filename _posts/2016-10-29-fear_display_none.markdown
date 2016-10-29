---
layout: post
title:  ".fear{display: none;}"
date:   2016-10-29 00:15:55 +0000
---


Just before quitting my job and starting down this path to become a web developer, I attended a small seminar by a friend who was working on a book about life transitions. One thing that stuck with me was how he spoke of "embracing the dark times" because there will surely be some. 

I knew that this journey would not be all laughter and smiles but his point was to roll with the punches. In all likeliness, you will get stuck or even angry at times when things aren't going as you'd expected. While it's important to have goals and ambitions, I've always felt comfortable having little to no exceptions such that I would never be disappointed. Riding the line between these two, I've done a damn swell job. Then I arrived at the section on AJAX...

A few weeks later and I'm a lot more comfortable understanding this aspect of JS and jQuery, but it's still a bit tricky at times especially when conforming to the conventions and configuration of how these new languages process. To say my transition from Ruby to JS has been bumpy would be quite an understatement. I do find comfort in learning from others that this is not uncommon. 

It's funny how you can look back at what you've learned and it all seems so obvious now, but at the time it felt like reading hieroglyphics. I definitely took a lesson from Ruby and made sure I was very comfortable with using `debugger` to follow the sequence of my code in the browser. After a while it almost became a game of catch, setting up parameters for an AJAX call in the browser using jQuery, attempting to hit my `binding.pry` in a controller action, then passing back just the information I need in just the right format so I could use it to mess with certain elements back in the browser. 

I can confidently say that adding jQuery elements to my Rails project, Questionable, has been the most fun I've had so far. It had been about a month since I completed that project and it was refreshing to pick it up again... Kinda like hanging out with a good friend you haven't seen in a while. I had to remind myself where everything was at first but the moment I added a new .js folder to my asset pipeline, setup `$(function(){..}` with a listener like `$('form.new_answer').submit(function(event){...}`, threw in a `debugger` and it saw that everything was working as expected, I was thrilled to say the least! 

That was 3 days ago and I feel like I've covered so much ground since then! I believe I had more epiphanies in this time than ever in my whole life! Here are just a few...

* Turbolinks can be more harm than good in some cases and I'm still not 100% on what it does...
* `preventDefault()` is a PITA to get right at times but I'm pretty sure it was all Turbolinks' fault.
* You can pass an entire partial render to an AJAX receiver function from the controller.
* `remote: true` is a god send but only if it's *allowed* to be used in a project ;) 
* You can send multiple serialized json objects to AJAX with `json: {question: @question, answer: @answer}` BUT if your answers `has_one` question, questions `has_many` answers, and you want to get all of @question's answers then you will need to send it without the curly brackets like so, `json [@question, @answer]`... 
* If you're going to use the AJAX response to insert, overwrite, or otherwise reload some buttons, which need to caught by your jQuery, you'll  have to *reapply* their listeners.
* Refactoring javascript isn't nearly as much fun as Ruby or HTML, but just as cathartic :P

Interestingly, I found the previous project of making a jQuery Tic Tac Toe game excruciating, yet building out my own app using the same techniques was some of the most fun I've had coding in months. The Pokemon CLI Gem I built early on was probably a close second ;)

All in all, I'm feeling stoked and ready to take on Angular! From my initial job hunting research, it seems like Ruby on Rails with jQuery is a basic requirement but Angular is where I earn my big boy pants. Wish me luck!

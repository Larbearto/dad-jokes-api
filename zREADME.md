Plan: Build a Dad Joke Application that gives the user a random joke from a button.

Requirements:

- 3rd party API from 'https://icanhasdadjoke.com/api
- Use the fetch API that is built into the browser to make a request and get an object with:

1. Id
2. a joke
3. a status

- That joke will then be used in the application to display.
- Build out the interface with HTML and CSS and JavaScript.
- In javascript I'll use async function with fetch.
- Because I'm using fetch I will use promises as well.

Need:
-Title
-Container that wraps h3 - don't laugh challenge

- div with id of joke, class of joke for styling.
- once we make the request and we're able to put the joke into the DOM and then we want to button to get another joke.
- button ID of jokeBtn with class of Btn for styling and say, Get another joke
- box shadow with 2 shadows, when active meaning when we click and hold i want to add a transform effect - use scale it from 1 to .98
  .btn:active {transform: scale(0.98)}
  .btn:focus {outline: 0}

API:

So the API we're working with an API is just application programming interface.
We're working with something called the JSON API.
It serves JSON data, which is essentially like a like a JavaScript object.

JSON has curly braces
JSON does use double quotes on the keys and the values,
but you can see this is just
an object with an ID, a joke and a status.

$ curl -H "Accept: application/json" https://icanhazdadjoke.com/
{
"id": "R7UfaahVfFd",
"joke": "My dog used to chase people on a bike a lot. It got so bad I had to take his bike AWAIT.",
"status": 200
}

So if we make an HTTP, request, a get request to this particular URL, we should get something like this.

{
"id": "R7UfaahVfFd",
"joke": "My dog used to chase people on a bike a lot. It got so bad I had to take his bike AWAIT.",
"status": 200
}

Now there's a few different formats.
The default is going to be HTML and we don't want that.
We want an application slash JSON.

So to get that, we actually have to send a header because when you send a HTTP request, you can send headers and we want to send a header of accept equal to application slash JSON.

And there's, there's many, many different ways to make requests.
We're going to be using fetch within our application.
You could even use Curl, which is a terminal program.

TERMINAL:
Paste: curl -H "Accept: application/json" https://icanhazdadjoke.com/

:: {"id":"ljGB5o49Elb","joke":"Dad, can you put my shoes on? I don't think they'll fit me.","status":200}

Each call I make is going to be a different joke because they're random jokes with a different ID.

POSTMAN:
Same with postman but only url.

If I make request without adding the accept header value, I'm going to get HTML back.
I want JSON back.
So I'm going to add in headers for a key.

Key:accept
value: application/json
if I send that, then I get JSON back.

So I just get this simple object just like you saw when I used Curl.

METHODS:
Get: getting data or something from the server
Post: you typically use when you're submitting data.
So if you're submitting like a contact form or maybe you have an admin screen where you're where you're adding a new blog post or something that would be a post request
PUT: is used for updating data that's on the server.
PATCHED: same as PUT
DELETE: delete data on the server.

But what we want to do is make that request from our application
Ee can do that by using the Fetch API.

So the Fetch API provides a JavaScript interface for accessing and manipulating parts of the HTTP pipeline, such as requests and responses.

And there's an example right here:
fetch('http://example.com/movies.json')
.then((response) => response.json())
.then((data) => console.log(data));

and it doesn't have to be a third party API like we're using. It could be your own back end.

So you could build an API with like Express Node.js and Express or Python, Django or PHP, Laravel or whatever it might be.
Or you can actually get just standard JSON files with fetch.

Now when you call fetch to a URL,
it returns a promise because it fetches the data asynchronously.

So you have this .then()
when it finishes and the fetch API is a little weird because you have
.then()'s,
the first one, you get the response and then you say, well, I want the JSON data.
So this is just an arrow function that we pass in and we're saying response JSON and then we have another dot.
Then because this returns a promise as well and that gives us the actual data.
So in this case, we would be logging the data that's in this movie's JSON file.
So this is a get request by default.
fetch('http://example.com/movies.json')
.then((response) => response.json())
.then((data) => console.log(data));

If you wanted to make a post or put request, you would you would pass in the URL just as we did above.
But then you'd have this extra options, value or object and you'd pass in the method that you want.
So in this case it's a post request, and if you are submitting form data, you would pass that in the body.
Like if you had a registration form with the name, email, password, that stuff would all go in the body.

// Example POST method implementation:
async function postData(url = '', data = {}) {
// Default options are marked with *
const response = await fetch(url, {
method: 'POST', // *GET, POST, PUT, DELETE, etc.
mode: 'cors', // no-cors, *cors, same-origin
cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
credentials: 'same-origin', // include, *same-origin, omit
headers: {
'Content-Type': 'application/json'
// 'Content-Type': 'application/x-www-form-urlencoded',
},
redirect: 'follow', // manual, *follow, error
referrerPolicy: 'no-referrer', // no-referrer, \*no-referrer-when-downgrade, origin, origin-when-cross-origin, same-origin, strict-origin, strict-origin-when-cross-origin, unsafe-url
body: JSON.stringify(data) // body data type must match "Content-Type" header
});
return response.json(); // parses JSON response into native JavaScript objects
}

postData('https://example.com/answer', { answer: 42 })
.then((data) => {
console.log(data); // JSON data parsed by `data.json()` call
});

And I'm not going to get too deep into this because what we're doing is pretty simple.
So we're going to make a get request to get our joke, put it in our interface or in our, you know, in our application.
I'm also going to show you afterwards how we can use a different syntax than this .then().

So there's something called a ASYNC, which makes it a little cleaner, at least in my opinion.
And I think it's it seems to be the more popular thing to do when using promises is to use a sync await rather than .then() because this can get quite messy.

And there's also a library called Axios, which I actually prefer over fetch, but fetch is built into the browser.
You don't have to add a CDN or install it or anything like that.

We'll also have this button.
Make another request to get another joke.

## --

- So I have my script JS And first thing I want to do is bring in what I need from the DOM.
  So we have our joke, I'm just going to call this joke l for joke element and set this to document dot
  get element by DX and that should have an ID of joke.
  So we're getting this div right here that wraps this text.
  So we're bringing that into our JavaScript.
  We also want the button.
  So let's say con's jokeBtn equals document dot get element by DX and I think I used joke BTN right here.
  So we're getting the button as well because we need an event listener on that.
  So right when we come into this application, we want to call a function called 'generate joke'.

So let's say function, generate joke and this is where we want to make our fetch request. Now, like I said, this is built into the browser.
It's, it's a native API so we don't have to include any kind of CDN or anything.
And what we want to do is make a fetch request to a specific URL, which is going to
'http://icanhazdadjoke.com'

Now, remember, if we just make a GET request to this without the accept header of applications json,
it's going to give us HTML and that's not what we want.

So we can add an an object here with a headers value
and headers is going to be an object and then we can put in for the key for the header that we want.

```
// USING ASYNC/AWAIT
function generateJoke() {
  fetch('https://icanhazdadjoke.com', {
    headers: {
      'Accept': 'application/json'
    }
  })
}
```

Remember when we were in Postman, they close us now.
So we in Postman I set a header of Accept as the key and application slash JSON is the value.
So we're doing the same thing here.
We're saying Accept as the key
and setting 'application/JSON' as the value.

Now usually what I like to do if I'm adding headers is or not even just headers, but anything in this object, I'll just take thisand put it in a variable.
So I'm going to cut 'const config' and I'll put it in a variable called config and right above it I'll just say const config equals that object. I just think it's cleaner.

```
// USING ASYNC/AWAIT
async function generateJoke() {
	const config = {
		headers: {
			Accept: 'application/json'
		}
	}

  	fetch('https://icanhazdadjoke.com', config)
		.then((res) => res.json())
		.then((data) => {
			jokeEl.innerHTML = data.joke
		})
}
```

But you can of course you can do what I just had here.
Now, remember, this is going to give us a promise back.
So we have to set this to .then().
And remember with the fetch API we get the response.
You can call this whatever you want response or I usually call it res and this is an arrow function
and we just want to call res JSON to get the JSON data.

And then the second .then() is going to give us the actual data.

So this is another arrow function and for now I'm just going to console.log what data gives us.

So this should run right AWAIT.
So I'm going to open up my console and what we get is an object with an ID, a joke and a status just like you saw with Curl, just like you saw with Postman.
It's all the same API. We're just hitting it with different methods, different technologies, postman, curl, fetch, whatever.

So what do we actually want to do with this?
We want to take the joke from this object and insert it here in the card.
So in this arrow function right here, instead of console logging, let's open up a code block and let's take the joke element that we brought in above and set the inner HTML.

```
const jokeEl = document.getElementById('joke')
const jokeBtn = document.getElementById('jokeBtn')

jokeBtn.addEventListener('click', generateJoke)

generateJoke()
```

Let's set that to not not just data, because data is the entire object.
We want data joke because we're accessing this .joke from this entire object.
And as soon as the page reloads, we see a joke here.
The next thing I want to do is just hook an event listener up to this button so that it calls generate joke again.
So let's go up here and just say joke button and we'll add an event listener on to it and we want to listen for a click.
And when that happens, we want to call generate joke.
And as soon as I save that, we get a different joke because whenever we save it's going to call this function.

And you can check your network tab as well to see any requests that you get.
I'm just going to dislocate this for a second.
And if I just reload this, this is going to show you any files that were loaded, like our stylesheet, our script.

JS But if we look at so if we look at type, you see this fetch right here, this, it made a call to
this URL.
I can has dad jokes and we can see a few things.
We see our response which is the, you know, the ID, the joke and the status.
We can also check out the headers.
So it was this is the request URL that was made.
It was a get request.
So that's the method.
The status code was 200.
What else, the remote address and then any headers down here.
So there's response headers and there's also request headers.
And in the request header, we should have this accept application JSON because we sent that that was,
you know, a result of what we sent within the OP.
And then there's a bunch of other stuff here as well.
So whenever you need to see data that you get back, when you make any kind of request, you can check
it out in the network tab.
So let's just attach reattach this.
So that's pretty much it.

## --

Our application is very small and simple, but it works and we are making a request to a third party API.
Now the next thing I want to show you is how to use a ASYNC AWAIT.
Because personally I don't like this .then() syntax.
I think it looks kind of messy and we can make it look like it's synchronous when it's really asynchronous because we have to use this because this could happen while something else is happening.

So the .then() basically says when this is finished, then do something.
So I'm going to actually comment.
I'm going to copy this and comment this out because I want to just do it again with ASYNC AWAIT.

Now, here, where we make our request, I'm going to get rid of just everything here and the .then().
And what we can do is set for this fetch right here.
I'll set a variable called res response, whatever you want to call it, and set it equal to to the fetch.
Now, remember, fetch is ASYNC, so we have to await until it's done fetching.
So we use the await keyword.

```
// USING ASYNC/AWAIT
async function generateJoke() {
	const config = {
		headers: {
			Accept: 'application/json'
		}
	}

	const res = await fetch('https//icanhazdadjoke.com', config)

	const data = await res.json()

	jokeEl.innerHTML = data.joke
}

```

Now, whenever you use a weights inside of a function, you have to label that function ASYNC.

That's why it's called the ASYNC AWAIT.

The function you label ASYNC and then any promises that you want to put into a variable, you're going to put this a weight before it.

Now, this is going to give us, just like we have down here, it gives us the response, but we need to call this resident JSON.

So what we would do in this case, using the Fetch API, we could set another variable called data and we could set that to res dot JSON.

However, this also returns a promise, so we have to await on that and then the data will be in that variable.

So again, we'll just go down here and I'm just going to copy this line and I'm going to set that jokeelement in our HTML to data and then the joke value.
So I'm going to save that.
And you can see it works the same exact way.

I think that this looks better and cleaner because instead of the .then()s, we're just basically setting
what we get back from fetch into a regular variable and then whatever we get back from JSON into a variable
and then we can just continue on.
We don't have to have this inside of a .then() and it's all preference.

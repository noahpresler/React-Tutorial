# Welcome – Here Is How This Shindig Will Go
<img align="left" src="http://i.imgur.com/cyEEJiw.png" width="240px">

By the end of this tutorial you will have built a web app which will allow you to add random memes, upvote and downvote them, all from React. It will look just like the image you see to the right :D

**Best part is, you don't need to install anything!** It doesn't matter what OS you have – all you need is a browser.

We have everything set up for you in a collection of CodePens. If you ever get lost or confused, you can take a look at the code pen with the solution for that step or just use it to go forward and follow along.

Here are the CodePens for **future** reference (keep following along for now): 
- [Step 0: Hello World!](http://codepen.io/noahpresler/pen/JEZdvz?editors=1010#0)
- [Step 1: My First Meme](http://codepen.io/noahpresler/pen/egKNbL?editors=1010)
- [Step 2: The Meme Component](http://codepen.io/noahpresler/pen/dNKYGG?editors=1010#0)
- [Step 3: The Mapping of the Memes](http://codepen.io/noahpresler/pen/YNvyGG?editors=1010#0)
- [Step 4: Upvotes and downvotes](http://codepen.io/noahpresler/pen/NdzbXd?editors=1010)
- [Step 5: Setting state, onclicks](http://codepen.io/noahpresler/pen/OWEbvX?editors=1010)
- [Step 6: Adding New Memes](http://codepen.io/noahpresler/pen/EZRNEd?editors=1010 )
- [Step 7: LifeCycle & Component Did Update](http://codepen.io/noahpresler/pen/QdxGZM?editors=1010)

# Quick Tour of Code Pen
<img align="right" src="http://i.imgur.com/WzcOh9d.png" width="350px">

Open up [Step 0: Hello World!](http://codepen.io/noahpresler/pen/JEZdvz?editors=1010#0) and have a look around.
It should look like the screenshot to the right.

On the left you'll see HTML, and on the right is Javascript – through this whole application you'll actually never change the HTML, we will create this all purely from Javascript.

In the JS side, click the chevron next to the line ```let memes = ....``` to collapse that variable so it takes up less space. It is a list of memes we will use later in the tutorial, but you will never edit it, so keep it collapsed for ease of coding.

Swag, that's the whole setup. Time for step 0! All the CSS is done for you, so just be sure to use our class names :)

# Step 0: Hello World [(codepen)](http://codepen.io/noahpresler/pen/JEZdvz?editors=1010#0)

###Fork the Code Pen! 

Click on fork in the top right of the CodePen UI. This will create your own version of this pen for you to access later! Click on the title "Step 0: Hello World" to rename it. 

When you click run, you'll notice that the bottom portion of the window, the equivalent of a browser, is filled with grey and the words "Hello World". 

Let's go over how this works. 

### App Component

First, checkout our 'App Component'

```javascript
class App extends React.Component {
  render() {
    return (
      <p>Hello World</p>
    );
  }
}
```

Componenets are the core of React. React components let you split the UI into independent, reusable pieces, and think about each piece in isolation. React components can be defined by subclassing ```React.Component``` as you see we do with ```extends React.Component```.

### The Component's Render Function

They key function for this step is the ```render``` function inside. This returns the HTML that will later get posted to the DOM and displayed in your borwser. 

The render function is called whenever the component is initially rendered and whenver state/props change (we will get into this part later!).

### Inserting the App into the DOM

So when does it actually get rendered and displayed to the browser? The very last line:

```js
ReactDOM.render(<App />, document.getElementById('app'));
```

This renders the App component into the element with id 'app', the only tag we have for our HTML! 

_fun fact: look at how we tell the render call to render the App componenet. By create React Componenet, **you just defined a custom HTML tag ```<App />```**_

# Step 1: My First Meme [(codepen)](http://codepen.io/noahpresler/pen/egKNbL?editors=1010)

React handles data through the state variable.  Each React component has its own state.  We’ll add a constructor setting the initial state. Lets initialize it to the first element in the variable ```memes```.

### Setting Initial State

```js
//constructor just like in java!
  //sets up initial state in this.state = 
  constructor(props) {
    super(props)
    this.state = memes[0];
  }
```

We can now access the data in this component by typing “this.state” followed by the names of the values in the meme variable.  To access the image link, type “this.state.url” and to access the caption, type “this.state.caption”

### Rendering a Meme

Now lets render a meme instead of hello world! To do this we will use React's special Javascript - JSX. JSX is a javascript preprocessor that lets us place HTML in our javascript.  You can use React without JSX, but JSX makes things a lot more elegant. Inside the HTML snippets, we’ll use {} the curly braces to inject javascript code inside the HTML snippets. 

We will create a meme div, with an `<h1>` tag for the caption and an img tag for the meme. We will set the content using `this.state` inside of the {} curly braces to inject our javascript. 

Edit the render function as follows:
```js
render() {
    return (
      <div className="meme">
        <h1>{this.state.caption}</h1>
        <img src={this.state.url}/>
      </div>
    );
  }
```

Run the code, and bang! You did it! :D

### class v className

Because class is a reserved word in javascript and can only be used for defining a new class in javascript, we'll use `className` to define classes for our HTML elements.  Be sure to use our classNames for free CSS 😊

# Step 2: The Meme Component [(codepen)](http://codepen.io/noahpresler/pen/dNKYGG?editors=1010#0)

This is great, but when we want to display more than one meme and adding functinoality like upvoting/downvoting each meme, we'll want to create a component just for it.  There's no point in writing it each time. 

### A New Component

So just like the App Component, we'll create a Meme Component that has the render function from `App`

```js
render() {
  return (
    <div className="meme">
      <h1>{this.props.caption}</h1>
      <img src={this.props.url}/>
    </div>
  )
}
```

Note how we changed the way we referenced caption and url.  Instead of using `this.state`, we used `this.props`.  Props are parameters that are passed to the component.  We will pass the props in from the App Component.

### Passing Props

Just like how we used a custom HTML tag for `<App />`, we'll use a custom HTML tag for our Meme Component, `<Meme />`.  Inside our `<App />` render function, we'll replace the HTML with this plus two props passed like normal HTML attributes.  

```js
render() {
  return (
    <Meme caption={this.state.caption} url={this.state.url} />
  );
}
```

### Adding Variety

When you run this, everything should look the same as before, so lets add some variety by setting the initial state to a random meme.  

```js
this.state = memes[Math.floor(Math.random() * memes.length)];
```

# Step 3: The Mapping of the Memes [(codepen)](http://codepen.io/noahpresler/pen/YNvyGG?editors=1010#0)

Next step: let's leverage the Meme component to display multiple memes with minimal code duplication.

For loops are so last decade.  Instead of looping over state to access all the memes in our meme variable, we take an array and a function and apply the function to every object in the array. This is called a map. Mapping doesn’t alter the original array, it returns a new array.  We can do this with an arrow, say whaaa?

```js
this.state.memes.map(meme => <Meme caption={meme.caption} url={meme.url}/>)
```

Once again, this is saying "for each meme in our variable, map it to the matching meme compomnenet and display it in my browser".

Your App render function will then be:

```js
render() {
  return (
    <div>
      {
        this.state.memes.map(meme => <Meme caption={meme.caption} url={meme.url}/>)
      }
    </div>
  );
}
```

When you click run, you should now see a whole feed of memes! Woohoo! 


# Step 4: Upvotes and Downvotes [(codepen)](http://codepen.io/noahpresler/pen/NdzbXd?editors=1010)
# Step 5: Setting State & OnClick [(codepen)](http://codepen.io/noahpresler/pen/OWEbvX?editors=1010)
# Step 6: Adding New Memes [(codepen)](http://codepen.io/noahpresler/pen/EZRNEd?editors=1010 )
# Step 7: React LifeCycle & ComponenetDidUpdate [(codepen)](http://codepen.io/noahpresler/pen/QdxGZM?editors=1010)

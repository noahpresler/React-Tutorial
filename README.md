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

In the JS side, click the chevron <i class="fa fa-caret-down" aria-hidden="true"></i> next to the line ```let memes = ....``` to collapse that variable so it takes up less space. It is a list of memes we will use later in the tutorial, but you will never edit it, so keep it collapsed for ease of coding.

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

The key function for this step is the ```render``` function inside. This returns the HTML that will later get posted to the DOM and displayed in your borwser. 

The render function is called whenever the component is initially rendered and whenver state/props change (we will get into this part later!).

_What's the **DOM**? **D**ocument **O**bject **M**odel. It's the browsers model of all html of elements, properties, and events. The HTML DOM is a standard for how to get, change, add, or delete HTML elements._

### Inserting the App into the DOM

So when does it actually get rendered and displayed to the browser? The very last line:

```js
ReactDOM.render(<App />, document.getElementById('app'));
```

This renders the App component into the element with id 'app', the only tag we have for our HTML! 

_Fun fact: look at how we tell the render call to render the App componenet. By create React Componenet, **you just defined a custom HTML tag ```<App />```**_

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

Let's update the state of `App` to be all of the memes.

```js
this.state = {memes: memes};
```

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

### Up/Down State
Since Meme is its own componenet, we can now add state to it. Our goal is to store the number of upvotes and downvotes.
Just like before we will use the constructor to do this in _in the meme component_

```js
  constructor(props) {
    super(props)
    this.state = {ups: 0, downs: 0};
  }
```

Here you see that state is a dictionary/json object. It has `ups` and `downs` as keys with integers (defaulting to 0) as values. 

### Adding Buttons & Displaying Values
We will now add to buttons - an upvote and downvote button - which display these state variables. Once more, we use the {} curly braces to inject the state into the HTML.

```js
render() {
  return (
    <div className="meme">
      <h1>{this.props.caption}</h1>
      <img src={this.props.url}/>
      <a className="up">Upvotes – {this.state.ups}</a>
      <a className="down">Downvotes – {this.state.downs}</a>
    </div>
  )
}
```
After running, you'll see a green and red button. They should have zeros next to them since we defaulted the counts to 0. 
We will make those functional in the next step! 

# Step 5: Setting State & OnClick [(codepen)](http://codepen.io/noahpresler/pen/OWEbvX?editors=1010)

We will now add onClick events to the buttons to trigger changes to the ups/downs state. 

###onClick Handler

An onClick event is declared as a simple attribute on any HTML tag like so: 

```js
<a onClick={() => {...some js here...}}
```

Inside the on click we use an arrow function to succinctly define a function that will trigger upon the click of that element. This is the same as:

```js
<a onClick={function(){...some js here...}}
```

###Setting State
For our purposes, when one of these links is clicked, we want to change the number of upvotes from its previous value to its previous value plus one. 

However, in react, we use `this.setState()` to update our state. **Do not do this.state = ...**. This special function updates the fields specified in the object passed as a parameter in state. On top of this, it triggers a re-render and UI updates. So we update the links as follows:

```js
<a className="up" onClick={function(){
            this.setState({ups: this.state.ups + 1})
          }}>Upvotes – {this.state.ups}</a>
        
<a className="down" onClick={() => {
    this.setState({downs: this.state.downs + 1})
  }}>Downvotes – {this.state.downs}</a>
```

###Run & Recap

When you run, you'll find that a click on the upvote udpates state AND updates the UI. What's going on under the hood is 
- Each key in the object passed to `setState` is overwritten in state
- In this case `this.state.ups` becomes `this.state.ups + 1`
- The render function is called again, state has been updated, and therefore we see the labels on our buttons incrament! 

Nice work! 

# Step 6: Adding New Memes [(codepen)](http://codepen.io/noahpresler/pen/EZRNEd?editors=1010 )
Really great - your meme componenet is done. Next, let's make this feed more dynamic by heading back to the App componenet. 

We will now add a button which onClick will add a new random meme to our feed. 

To do this, we will use the onClick attribute you just learned about, the special `setState` function, and a special url that returns random images (http://lorempixel.com/300/200/).

Here's how it comes together:
- onClick we need to pass a new list of memes to overwrite the `memes` key in state. 
- This list should include all the old memes plus one new meme.
- We can create this new array using concat. ```this.state.memes.concat({url: 'http://lorempixel.com/300/200/' ,caption: 'Look! A new Meme!'})```
- Concat returns the old array with the new meme appendend (with a random img and a 'Look! A new Meme! caption)
- Sate gets updated, and just like last time a render is called so the UI updates! 

To add the button your code should look like the following:
```js
<a className="add" onClick={() => { 
      this.setState({memes: this.state.memes.concat({
                      url: 'http://lorempixel.com/300/200/',
                      caption: 'Look! A new Meme!'
                    })})
    }}>Add a Meme!
</a>
```

# Step 7: React LifeCycle & ComponenetDidUpdate [(codepen)](http://codepen.io/noahpresler/pen/QdxGZM?editors=1010)

## Beyond Render

In this tutorial we have focued on React Components. All of our components have extended `React.Component` and as a result we gained the capabilities of `render()` and `setState`. 

In fact, `render()` has been the only way which we have updated the UI.  

However, React Components have several such methods which form **The React Lifecycle**.

Each component has several "lifecycle methods" that you can override to run code at particular times in the process. Methods prefixed with **will** are called right before something happens, and methods prefixed with **did** are called right after something happens.

The [React Documentation](https://facebook.github.io/react/docs/react-component.html) details the methods: 

<img align="left" src="http://i.imgur.com/44UAknj.png" />

##ComponentDidUpdate

Let's give one of these lifecycle methods a spin.

The method `componentDidUpdate` is called right after an update occurs to a component. That is: when `this.props` or `this.state` is changed. 

**Pop quiz: where in the App componenet does this occur?**
Answer: when we add a new Meme - in this instance the state is updated with an additional meme in the array. 

So, for our foray into this lifecycle method, let's have the component scroll down to the newly added array when this occurs! 

We will use simple JQuery to do so: 
```
componentDidUpdate(prevProps, prevState) {
  $('body').scrollTop($('body').prop("scrollHeight")); 
}
```

Give it a run - if all is well, you'll see that when the App component gets updated (When you click the add meme button) it scrolls to the new one :D

# Afterword
Good luck and great work on the Tutorial. 

####To learn more: 
Learn More React: https://egghead.io/courses/react-fundamentals
Learn Redux: https://egghead.io/courses/getting-started-with-redux

####What's Redux? 
Redux is a methodology for React development in which there is one global state store rather than a store in each component.

####How to setup a React enviroment locally:
React with Webpack: http://survivejs.com/webpack/advanced-techniques/configuring-react/
React with Gulp: https://jonsuh.com/blog/integrating-react-with-gulp/

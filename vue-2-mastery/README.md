# Introduction

# Vue Instance

```js
// Syntax 
var app = new Vue ({options})

// Example
const app = new Vue ({
    el: "#app",
    data: {
        product: "socks",
        description: "a pair of socks"
    }
})

// On console.log(), you can acess app.product app.description
```

```yaml
On console.log(), you can acess "product" with app.product and "a pair of socks" with app.description
```

# Vue Expressions

- Expressions are a way of displaying data on the DOM. It is usually represented with `{{ }}`

```js
example
<div id="app">
    <h2>{{ product }}</h2>
</div>
```

# Attribute Binding 

```js
// Notes
1. v-bind dynamically binds an attribute to an expression
2. "src" is the attribute and "image" is the expression

// Example
v-bind:src="image"

// Notes
- Shorthand for v-bind can just be :src="image"
- Other attributes are
1. v-bind:alt="description" or :alt="description"
2. v-bind:href="url" or :href="url"
3. v-bind:title=
4. :class="isActive"
4. :style="isDisabled" etc
```

# Conditional Rendering

```js
// main.js
const app = new Vue ({
    el: "#app",
    data: {
        ...
        inStock: true
        inventory: 5
    }
})

// html
<p v-if="inStock">In stock</p>              // Will render this
<p v-else>Out of stock</p>
<p v-if="inventory<5">In stock</p>
<p v-if-else="inventory>=5">More in stock</p>

// Notes
- v-if will always add or remove elements from the DOM

- If place of "v-if", you can toggle the visibility of an element with "v-show"

- If "greet" is false, then v-show will automatically hide the element "<p>Hello, world</p>" in the DOM

```

# List Rendering

```yaml
- Display a list of Items from an array
```

```js
// An Array
 const app = new Vue ({
    el: "#app",
    data: {
        ...
        details: ["80% cotton", "20% polyster", "Gender-neutral"],
    }
})

// Syntax in html
<ul>
    <li v-for="detail in details">{{ detail }}</li>
</ul>

// Note 
For an iteration of items, user a key to identity each item

// Example of iterables
variants: [
    {
        variantId: 2,
        variantColor: "green"
    },
    {
        variantId:3,
        variantColor: "blue"
    }
]

// In html
<ul>
    <li v-for="variant in variants" :key="variant.variantId">{{ variant.variantId }}
    </li>
</ul>

```

# Event Handling

```js
- Listens for events that are specified

// Syntax
- v-on:<event-name>
<button v-on:click="addToCart"></button>

- A short-hand for "v-on" is "@" sign followed by the type of event (@click, @mouseover, @submit @keyup.enter etc)
```

# Class and Style Binding

```yaml
- Class and Style binding basically refers to binding an element to a css style

- In this case, we gonna bind the style to the css class "color-box"
```

```js
// Example: This color will evaluate to red
<h1 :style="{ color: color }"></h1> 

// js
data: {
    color: "red"
    fontSize: "12px"
}

// You can take a whole object
<h1 :style="styleObject"></h1>

// Or a list of styleObjects
<h2 :style="[styleObject, styleObject2]"></h2>

// Evaluates to:
<h1 style="color: red; fontSize: 10px"></h1>

//js
data: {
    styleObject: {
        color: "red",
        fontsize: "10px"
    }
    styleObject: {
        margin: "4px",
        padding: "20px"
    }
}
```

# Disabling Buttons

```yaml
- We want to disable a button if a condition is false

- If items are out of stock (inStock=false or !inStock), the disable the "Add to Cart" button

```

```js
// Add a :disabled bind to the "Add to cart" button
<button> @click="AddtoCart" :disabled="!isStock">Add to cart</button>
```

```js
// Assuming you want to add custom styling to the "Add to cart" button if the "inStock" is false (!inStock)

// This calls the .disabledButton css class and bind it to when inStock is not true (!inStock)

<button
    @click="AddToCart" 
    :disabled="!inStock">
    :class="{ disabledButton: !inStock}"
    Add to cart
></button>
```

# Computed Properties

```yml
- Computed properties is an option to the Vue object that compute values using other data properties of the Vue object
```

```js
// compute the name of the product
// NB: Computed properites are catched and thus good, it you don't want to perform expensive tasks

...
data: {
    brand: "Vue",
    product: "Tutorial"
},

computed: {
    title () {
        return this.brand + ' ' + this.product
    }
}
```

```yaml
- We gonna refactor code for hovering and changing the image

- We'll set an index with the 2-items we hover over
```

```js
// Event handling: html section
<div v-for="(variant, index) in variants" 
    :key="variant.variantId" 
    class="color-box"
    v-bind:style="{ backgroundColor: variant.variantColor }">
    <p @mouseover="updateProduct(index)">{{ variant.variantName }}</p>
</div>
```

# Components
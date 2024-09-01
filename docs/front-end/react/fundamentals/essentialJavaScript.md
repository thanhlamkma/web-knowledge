---
sidebar_position: 1
---

# Essential JavaScript for React

## 1. Destructuring Objects and Arrays

```tsx
const book = getDetailBook(2);

const { title, author, pages, publicationDate, genres } = book;

const [primaryGenre, secondaryGenre] = genres;
```

## 2. Rest/Spread Operator

A rest element must be last in a destructuring pattern

```tsx
const { title, author, ...otherInfo } = book;

const [primaryGenre, ...otherGenre] = otherInfo.genres;

const newGenres = [...otherInfo.genres, "epic fantasy"];

const updatedBook = { ...book, title: "New title" };
```

**Applications with Shallow Copy**

> **Shallow Copy:**
>
> > Creates a new object but _**references the same underlying values**_ as the original object.
> > Changes to the original object _**will also reflect**_ in the copied object for nested objects or arrays.
> >
> > ```js
> > // Shallow copy
> > const originalObject = {
> >   name: "Alice",
> >   age: 30,
> >   hobbies: ["reading", "painting"],
> > };
> > const shallowCopy = { ...originalObject };
> >
> > originalObject.hobbies.push("coding");
> > console.log(shallowCopy.hobbies); // Output: ["reading", "painting", "coding"]
> > ```
>
> **Deep Copy:**
>
> > Creates a new object and _**recursively copies all nested**_ objects and arrays, _**creating new instances**_ of each value.
> > Changes to the original object _**will not affect**_ the copied object.
> >
> > ```js
> > // Deep copy
> > const deepCopy = JSON.parse(JSON.stringify(originalObject));
> >
> > originalObject.hobbies.push("traveling");
> > console.log(deepCopy.hobbies); // Output: ["reading", "painting"]
> > ```
>
> **When to Use Which:**
>
> > _Shallow Copy_: Use when you want to create a new object with the same references to nested objects or arrays. This is often used for performance reasons, as it's faster than a deep copy.
> >
> > _Deep Copy_: Use when you need to create a completely independent copy of an object, including all nested objects and arrays. This is useful when you want to modify the copy without affecting the original object.
>
> **Additional Considerations:**
>
> > _Custom Objects_: For custom objects with methods or prototypes, you might need to use a more complex deep copy mechanism to handle these properties correctly. Libraries like Lodash or Ramda provide helper functions for deep copying complex objects.
> >
> > _Performance_: Deep copying can be more expensive than shallow copying, especially for large objects. Consider the trade-off between performance and the need for a completely independent copy.

## 3. Template Literals

```js
const summary = `${title}, a ${pages}-page long book, was written by ${author} and published in ${
  publicationDate.split("_")[0]
}`;
```

## 4. Ternaries Instead of if/else Statements

```js
const pagesRange = page > 1000 ? "over a thousand" : "less than 1000";

console.log(`The book has ${pagesRange} pages`);
```

## 5. Arrow function

```js
const getYear = (string) => {
  return string.split("-")[0];
};
```

## 6. Short-circuiting and Logical operators: &&, ||, ??

Falsy values in JavaScript are values that are considered false when used in a Boolean context. These values include:

- `false`
- `0`
- `null`
- `undefined`
- `''` (empty string)
- `NaN` (Not a Number)

<table>
  <thead>
    <tr>
      <th>Logical AND (&&)</th>
      <th>Logical OR (||)</th>
      <th>Nullish Coalescing (??)</th>
    </tr>
  </thead>
  <tr>
    <td colSpan="3">
      Evaluates its operands from left to right.
    </td>
  </tr>
  <tr>
    <td>
      - Returns the first falsy value it encounters or the last operand if all are truthy.
      - Short-circuits evaluation: If the first operand is falsy, it doesn't evaluate the second.
    </td>
    <td>
      - Returns the first truthy value it encounters or the last operand if all are falsy.
      - Short-circuits evaluation: If the first operand is truthy, it doesn't evaluate the second.
    </td>
    <td>
      - Returns the first operand if it's not null or undefined; otherwise, it returns the second operand.
      - Short-circuits evaluation: If the first operand is not null or undefined (_mean it can be other false values - 0, ""_), it doesn't evaluate the second.
    </td>
  </tr>
</table>

**Example**

```js
// Operator &&
console.log(true && "Something"); // Something
console.log(false && "Something"); // false
console.log("Hello" && "Something"); // Something
console.log(0 && "Something"); // 0

// Operator ||
const spanishTranslation = book.translations.spanish || "NOT TRANSLATED"; // NOT TRANSLATED
const totalReviews = book.reviews.length || "No review"; // No review

// Operator ??
const totalReviews = book.reviews.length ?? "No review"; // 0 => What difference between ?? and || ?
```

## 7. Optional Chaining

```js
function getTotalReviewCount(book) {
  const goodReviews = book.goodReviews.count;
  const badReviews = book.badReviews?.count ?? 0; // If not using optional chaining, the error will be happened
  return goodReviews + badReviews;
}
```

## 8. Array

### Map Method

```js
const essentialData = books.map((book) => {
  return {
    title: book.title,
    author: book.author,
  };
});

// OR

const essentialData = books.map((book) => ({
  title: book.title,
  author: book.author,
}));
```

### Filter Method

```js
const longBooks = books
  .filter((book) => book.pages > 500)
  .filter((book) => book.hasMovieAdaptation);

const adventureBooks = books
  .filter((book) => book.genres.includes("adventure"))
  .map((book) => book.title);
```

### Reduce Method

```js
const pagesAllBooks = books.reduce((acc, book) => acc + book.pages, 0);
```

### Sort Method

This method is unlike the map, filter, and reduce method.
This is **not a functional method**. It is actually a mutating method, so it changes the original array.

So when using the sort method, you should copy the array firstly by using `slice()` method.
Because `slice()` with no arguments will create new array like original array

```js
const arr = [3, 5, 1, 9, 8];

const sorted = arr.slice().sort((a, b) => a - b);

console.log(sorted); // [1, 3, 5, 8, 9]
console.log(arr); // [3, 5, 1, 9, 8] - if not using slice, 'arr' will be [1, 3, 5, 8, 9]
```

### Immutable Array

It's quite important to know how to add element to array, how to delete elements, and also to update elements all without mutating the original underlying array.

```js
const newBook = {
  id: 6,
  title: "Harry Potter and the Chamber of Secrets",
  author: "J. K. Rowling",
};

// 1) Add newBook object to array
const bookAfterAdd = [...books, newBook];

// 2) Delete book object from array
const bookAfterDelete = bookAfterAdd.filter((book) => book.id !== 3);

// 3) Update book object
const bookAfterUpdate = bookAfterDelete.map((book) =>
  book.id === 1 ? { ...book, pages: 1200 } : book
);
```

## 9. Asynchronous JavaScript

### Promises

- JS needs to do an HTTP request, needs to wait until that request is processed and then it needs to download that data basically from this server. Therefore, JS using `fetch` API to handle the issue.

- **Fetch** is a built-in JavaScript API that provides a way to make network requests to servers. It's a more modern and flexible alternative to the traditional.

- Key Features of Fetch:

  > **Promises**: Fetch returns a Promise, which allows for asynchronous operations and easy handling of success and error cases.

  > **Flexibility**: Fetch can be used to make various types of requests, including GET, POST, PUT, DELETE, etc.

  > **Options**: It provides options for customizing requests, such as headers, body content, and credentials.

```js
fetch("https://jsonplaceholder.typicode.com/todos/1'")
  .then((response) => {
    if (!response.ok) {
      throw new Error(
        "Network response was not ok (status: ${response.status})"
      );
    }
    return response.json();
  })
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

### Async/Await

`async/await` in JavaScript is a syntactic sugar that makes working with asynchronous operations, such as promises, **more readable and easier** to understand. It provides a way to write asynchronous code in a more synchronous-looking style.

`async` keyword:

- Declares a function as asynchronous.
- Indicates that the function may return a Promise.

`await` keyword:

- Can only be used within an async function.
- Pauses the execution of the function until the Promise resolves and returns its value.

```js
async function getTodoList() {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos");
    const data = await response.json();
    return data;
  } catch (error) {
    console.error("Error:", error);
    return [];
  }
}

const todoList = getTodoList();
```

**Benefits of using `async/await`:**

- **Improved readability**: Code becomes more linear and easier to follow.
- **Simplified error handling**: try...catch blocks can be used to handle errors in a more straightforward way.
- **Better performance**: In some cases, `async/await` can improve performance compared to using Promises directly.

**Key points to remember:**

- `async/await` is a syntactic sugar, not a new feature. It's based on Promises. You can only use `await` within an `async` function.
- `await` pauses the execution of the function until the Promise resolves.
- `async/await` makes asynchronous code more readable and easier to understand.

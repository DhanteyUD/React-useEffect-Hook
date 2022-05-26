# Fetch Data from an API

Learn the basics of asynchronous functions and promises by fetching data from an API using fetch, useEffect and useState

---

### Step 1

Import useEffect at the top of your file.

```js
import React, { useEffect } from 'react';
```

... define your useEffect hook inside of your component.

```js
import React, { useEffect } from 'react';

const App = () => {
  useEffect(() => {
    // Fetch API here
  }, []);

  return <div>{Display response here}</div>;
};

export default App;
```

---

### Step 2

Define your URL

> When a user lands on a page, he want to call the API. In other words, you want to call the API during the mounting part of the component's lifecycle.
>
> The API url you want to get a data from would look like this: `https://api.random-data.com/data`. You will save it in a variable inside of the `useEffect` hook.

```js
useEffect(() => {
  const url = 'https://api.random-data.com/data';
}, []);
```

---

### Step 3

Create asynchronous function

> ...Then, create an asynchronous function to fetch your data. An asynchronous function is a function that needs to wait after the promise is resolved before continuing. In your case, the function will need to wait after the data is fetched (our promise)
> before continuing.

```js
const fetchData = async () => {
  try {
    const response = await fetch(url);
    const json = await response.json();
    console.log(json);
  } catch (error) {
    console.log('error', error);
  }
};
```

Put the fetchData function above in the `useEffect` hook and call it, like so:

```js
useEffect(() => {
  const url = 'https://api.random-data.com/data';

  const fetchData = async () => {
    try {
      const response = await fetch(url);
      const json = await response.json();

      console.log(json);
    } catch (error) {
      console.log('error', error);
    }
  };

  fetchData();
}, []);
```

> The function created is wrapped in a try...catch statement so that the function catches the errors and prints them in the > console. This helps debug and prevents the app to crash unexpectedly.
>
> Inside of the try, we are using the built-in fetch API from JavaScript to get the data from the data API.
> We put the await keyword just in front of it to tell the function to wait for the fetch task to be done before running the next > line of code.
>
> Once we get a response, we are parsing it using the .json() function, meaning that we are transforming the response into JSON > data that we can easily read. Then, we are printing the JSON data in the console.

---

### Step 4

Get the data

At this point, if you check in the console, you would have gotten the data from the API. We only want the data so we will print it using the below:

```js
console.log(json.data);
```
---

### Step 5

Save the data in a local state

> Now you should have gotten the actual data, you can save it into a local state using the useState hook.

Import `useState` and define it.

```js
import React, { useEffect, useState } from 'react';

const [data, setData] = useState('');
```

Then, instead of printing the data in the console, save it in the data state.

```js
setAdvice(json.data);
```
---

### Step 6

To display the data, simply call the data state in your return body:

```js
return (
  <div>
    <p>{advice}</p>
  </div>
);
```

---

## Final code with styling

The final code will look like so:

```js
import React, { useEffect, useState } from 'react';

const App = () => {
  const [data, setData] = useState('');

  useEffect(() => {
    const url = 'https://api.random-data.com/data';

    const fetchData = async () => {
      try {
        const response = await fetch(url);
        const json = await response.json();

        console.log(json.data);
        setAdvice(json.data);
      } catch (error) {
        console.log('error', error);
      }
    };

    fetchData();
  }, []);

  return (
    <Wrapper>
      <Paragraph>{data}</Paragraph>
    </Wrapper>
  );
};

export default App;
```

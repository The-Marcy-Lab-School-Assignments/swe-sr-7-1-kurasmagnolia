<!-- @format -->

# Technical Writing Assignment

For guidance on setting up and submitting this assignment, refer to the Marcy lab School Docs How-To guide for [Working with Short Response and Coding Assignments](https://marcylabschool.gitbook.io/marcy-lab-school-docs/fullstack-curriculum/how-tos/working-with-assignments#how-to-work-on-assignments).

## Prompt 1

In your own words, explain why React is a popular choice for building user interfaces. Make sure to mention at least one benefit, such as how it simplifies development, supports reusable components, or helps optimize performance. Feel free to include any specific features you find particularly helpful.

### Response 1

React is a popular choice among developers for building user interfaces because of its **component-based architecture**, where UIs (user interfaces) are broken down into reusable parts called components. You can think of them like lego blocks, where each part is **modular** and can be stacked on one another to build larger, more complex structures. Additionally, each component is self-contained, meaning that it has its own logic, behavior, and styles, but can still connect with other components to build a full UI, just like how individual Lego bricks can interlock to form something bigger.

One major benefit of this approach is that it simplifies writing code byfollowing the **DRY** principle (**D**on't **R**epeat **Y**ourself), reducing repetitive code and making applications more maintainable and scalable. This leads to cleaner, readable, and dynamic code.

A specific feature I find particularly helpful is React Router, which allows seamless navigation between different pages in an application without actually going to the page, but updates the current page we're on with the component we want to see, improving performance and providing a smoother user experience.

## Prompt 2

Explain how the useState hook is used in React to manage state within functional components. In your response, include an example of how useState might be used in a simple application and why managing state is important in building interactive user interfaces.

### Response 2

## Prompt 3

Describe the different ways the useEffect hook can be triggered in a React component. Include an explanation of how the dependency array influences its behavior. If possible, provide a code example for each scenario to illustrate your explanation.

### Response 3

## Prompt 4

The component below makes a mistake when using useEffect. When running this code, we will get an error from React! Please fix this code.

```js
const DogDisplay = () => {
  const [imgSrc, setImgSrc] = useState(
    'https://images.dog.ceo/breeds/hound-english/n02089973_612.jpg'
  );

  useEffect(async () => {
    try {
      const response = await fetch('https://dog.ceo/api/breeds/image/random');
      if (!response.ok) throw new Error(`Error: ${response.status}`);
      const data = await response.json();
      setImgSrc(data.message);
    } catch (error) {
      console.error(error);
    }
  }, []);

  return <img src={imgSrc} />;
};
```

After fixing the code provide and explanation to what you fixed and why it needed to be fixed.

### Response 4

What I fixed within the code was defining an async function inside of the `useEffect` and calling it instead of making the `useEffect` callback **asynchronous**. The reason for that is because `useEffect` doesn't support support **asynchronous** functions directly, and expects a **synchronous** cleanup function. When it's made **asynchronous** instead, it returns a **Promise** instead of a cleanup function, which React wouldn't know what to do with it.

_*Fixed code:*_

```jsx
const DogDisplay = () => {
  const [imgSrc, setImgSrc] = useState(
    'https://images.dog.ceo/breeds/hound-english/n02089973_612.jpg'
  );

  useEffect(() => {
    const fetchDogImage = async () => {
      // new defined async function for fetching
      try {
        const response = await fetch('https://dog.ceo/api/breeds/image/random');
        if (!response.ok) throw new Error(`Error: ${response.status}`);
        const data = await response.json();
        setImgSrc(data.message);
      } catch (error) {
        console.error(error);
      }
    };

    fetchDogImage();
  }, []);

  return <img src={imgSrc} alt="Random Dog" />;
};
```

# React in TypeScript

## useState in TypeScript - string/boolean/number

```ts
const [county, setCounty] = useState<string>("los angeles");
const [loading, setLoading] = useState<boolean>(false);
const [age, setAge] = useState<number>(0);
```

## useState in TypeScript - array

```ts
const [statesList, setStatesList] = useState<string[]>([]);
```

## useState in TypeScript - object

```ts
interface IFormValues {
  us_state: string;
  us_county: string;
}

const [formValues, setFormValues] = useState<IFormValue>({
  us_state: "",
  us_county: "",
});
```

# useState updater function does not reflecting change immediately

- The state update using the updater provided by useState hook is also asynchronous, and will not be reflected immediately.

```js
setMovies(result);
console.log(movies); // movies here will not be updated
```

- If you want to perform an action on state update, you need to use the useEffect hook, much like using componentDidUpdate in class components since the setter returned by useState doesn't have a callback pattern

```js
useEffect(() => {
  // action on update of movies
}, [movies]);
```

- However, if you want to merge the response with the previously existing values, you must use the callback syntax of state updation along with the correct use of spread syntax like

```js
setMovies((prevMovies) => [...prevMovies, ...result]);
```

**References:**

- https://stackoverflow.com/questions/54069253/usestate-set-method-not-reflecting-change-immediately

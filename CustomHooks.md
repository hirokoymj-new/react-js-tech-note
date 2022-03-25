# Creating Custom Hooks: useFetch.ts

- Creating custom hook to call axios API in TypeScript.

### useFetch.ts

```ts
import { useEffect, useState } from "react";
import axios from "axios";

export const useFetch = <R extends any = any>({ method, url }: any) => {
  const [data, setData] = useState<R | null>(null); // set `R` as returned type
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

  useEffect(() => {
    setLoading(true);
    axios({ url, method })
      .then((response) => {
        setData(response.data);
      })
      .catch((err) => {
        setError(err);
      })
      .finally(() => {
        setLoading(false);
      });
  }, [url, method]);

  const refetch = () => {
    // refetch function is used when you want to trigger API.
    setLoading(true);
    axios({ url, method })
      .then((response) => {
        setData(response.data);
      })
      .catch((err) => {
        setError(err);
      })
      .finally(() => {
        setLoading(false);
      });
  };

  return { data, loading, error, refetch };
};
```

### How to use useFetch.ts

```ts
const { data, loading, error, refetch } = useFetch<string[]>({
  url: "https://corona.lmao.ninja/v2/historical/usacounties",
  method: "get",
});

// JSX
return (
  <div>
    {loading ? (
      <p>...loading</p>
    ) : (
      <p>
        {data?.map((d) => (
          <li>{d.name}</li>
        ))}
      </p>
    )}
  </div>
);
```

- `refetch` is used when you want to trigger axios API. For examle when you click a button, a api calls.

Example:

```js
const { data, loading, error, refetch } = useFetch<string[]>({
  url: "https://corona.lmao.ninja/v2/historical/usacounties",
  method: "get",
});

useEffect(() => {
  refetch();
}, [us_state]);

// JSX
return <button onClick={refetch}>search</button>;
```
## How to make easier to render function in React. 
- Use/built re-useable components. Use `Children` prop in a re-usable component so the Children part will be act as a template you can insert any HTMLs.
- Select a nice hooks package to make easier to render. For example REST apis, I use useAxios. For form I use React-Hook-Form.
- If you find similar features in multiple pages, consider to create custom Hooks.


### References:

- [StackOverFlow: useFetch hook with typescript and axios](https://stackoverflow.com/questions/65651772/usefetch-hook-with-typescript-and-axios)
- [Clean API Call With React Hooks](https://betterprogramming.pub/clean-api-call-with-react-hooks-3bd6438a375a)

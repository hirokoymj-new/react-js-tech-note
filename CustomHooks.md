# Creating Custom Hooks: useFetch.ts

- Creating custom hook to call axios API in TypeScript.

### useFetch.ts

```js
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

  const refetch = () => { // refetch function is used when you want to trigger API.
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

```js
const { data, loading, error, refetch } = useFetch<string[]>({
  url: "https://corona.lmao.ninja/v2/historical/usacounties",
  method: "get",
});
```

- `refetch` is used when you want to trigger axios API. For examle when you click a button, a api calls.

Example 1

```js
<button onClick={refetch}>search</button>
```

Example 2

```js
useEffect(() => {
  refetch();
}, [us_state]);
```

### References:

- [StackOverFlow: useFetch hook with typescript and axios](https://stackoverflow.com/questions/65651772/usefetch-hook-with-typescript-and-axios)
- [Clean API Call With React Hooks](https://betterprogramming.pub/clean-api-call-with-react-hooks-3bd6438a375a)

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

# React.js

## Pass down onClick props to child component

**App.js (Parent component)**

```js
const App = () => {
  const onItemClick = (country: Country) => {
    const found = activeCountry.find(
      (d) => d.CountryCode === country.CountryCode
    );
    if (found) {
      const result = activeCountry.filter((d) => d.Country !== country.Country);
      setActiveCountry([...result]);
    } else {
      setActiveCountry([...activeCountry, country]);
    }
  };

  return (
    <CountryList
      countries={data.Countries}
      onItemClick={onItemClick} // Pass down onClick funtion to Card component.
      activeCountry={activeCountry}
    />
  );
};
```

**CountryList.js (A child component)**

```js
export const CountryList = ({ onItemClick }) => {
  return (
    <>
      {countries.map((d) => {
        return (
          <Card key={d.CountryCode} onClick={() => onItemClick(d)}>
            //onClick calls HERE!!
            <Typography variant="subtitle1">{d.Country}</Typography>
          </Card>
        );
      })}
    </>
  );
};
```

# The Difference Between Query and Route Parameters in API Calls

# 1. Query Parameter (First URL)

```
http://localhost:7009/api/finance/summary-of-daily-collection/getById?id=8c03a9a1-72f0-4d92-abf9-a9c981d703f3
```

* Here, the id is passed as a query parameter using ?id=.
* This is typically used for optional parameters or when multiple parameters need to be passed.

## Backend (Express.js)

```js
app.get('/api/finance/summary-of-daily-collection/getById', (req, res) => {
    const { id } = req.query; // Access query parameter
    res.send(`Received ID: ${id}`);
});
```

## Frontend (Axios Fetch Example)
```js
const id = "8c03a9a1-72f0-4d92-abf9-a9c981d703f3";
axios.get(`http://localhost:7009/api/finance/summary-of-daily-collection/getById?id=${id}`)
  .then(response => console.log(response.data))
  .catch(error => console.error(error));
```
# 2. Route Parameter (Second URL)
```
http://localhost:7009/api/finance/summary-of-daily-collection/getById/8c03a9a1-72f0-4d92-abf9-a9c981d703f3
```

* Here, the id is passed as a route parameter (part of the URL path).
* This is typically used when an identifier is required and directly part of the resource path.

## Backend (Express.js)
```js
app.get('/api/finance/summary-of-daily-collection/getById/:id', (req, res) => {
    const { id } = req.params; // Access route parameter
    res.send(`Received ID: ${id}`);
});
```
## Frontend (Axios Fetch Example)
```js
const id = "8c03a9a1-72f0-4d92-abf9-a9c981d703f3";
axios.get(`http://localhost:7009/api/finance/summary-of-daily-collection/getById/${id}`)
  .then(response => console.log(response.data))
  .catch(error => console.error(error));
```

# When to Use Which?

* Use query parameters (?id=...) when the parameter is optional or when multiple filters are needed.

* Use route parameters (/getById/:id) when the parameter is mandatory and directly identifies a resource.

# Why Use ?.? (called Optional Chaining (?.) )
* ?. helps prevent runtime errors when accessing properties of undefined or null values.

## How ?. Works in response?.data?.data
### Example Without Optional Chaining (🚨 Error-Prone)
```javascript
const response = null; // API response is null (failed request)

console.log(response.data.data); // ❌ Throws an error: Cannot read properties of null (reading 'data')
```
### Example With Optional Chaining (✅ Safe)
```javascript
const response = null; // API response is null

console.log(response?.data?.data); // ✅ Doesn't throw an error, just returns 'undefined'
```

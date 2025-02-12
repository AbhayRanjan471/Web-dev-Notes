# How navigate work
## 1st Page
- when the **hadleView button** is clicked we are calling the handleView function and sending  `receipt` as an argument
  ```html
  <button
    onClick={() => handleView(receipt)}
    className="text-blue-600 mr-2"
  >
  ```
- It uses `navigate()` : navigate() is from React Router, used to programmatically redirect to another page.
- In this while navigating we are passing the data to the next page
```javascript
const handleView = (receipt) => {
  navigate(`/register-refund-remission-writeoff/${receipt.id}`, {
    state: { receipt, activeTab },
  });
};
```
- Passing Data (state) to the Next Page
```javascript
{
  state: { receipt, activeTab }
}
```
-- The `state` object passes `receipt` and `activeTab` to the new page.
-- The new page can access this data via **location.state**.

## 2nd page
### Accessing Data in the New Page
```javascript
import { useLocation } from "react-router-dom";

const RefundRemissionPage = () => {
  const location = useLocation();
  const { receipt, activeTab } = location.state || {}; // Get passed data

  return (
    <div>
      <h1>Receipt ID: {receipt?.id}</h1>
      <p>Status: {receipt?.status}</p>
      <p>Active Tab: {activeTab}</p>
    </div>
  );
};

```
- **useLocation().state** retrieves the `receipt` & `activeTab` passed from the previous page.

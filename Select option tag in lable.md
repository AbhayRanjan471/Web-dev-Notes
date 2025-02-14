```javascript
import React, { useState } from "react";

const YearSelector = ({ setValue }) => {
  // State for manual year input and selected year
  const [customYear, setCustomYear] = useState(""); // For manual year input
  const [selectedYear, setSelectedYear] = useState(""); // Stores displayed value
  const currentYear = new Date().getFullYear(); // Get current year

  // Handle dropdown selection change
  const handleYearChange = (event) => {
    const selectedValue = event.target.value;
    let calculatedYear = selectedValue; // Default to selected value

    if (selectedValue === "Arrears") {
      calculatedYear = "Arrears"; // Keep text
    } else if (selectedValue === "other") {
      calculatedYear = ""; // Allow manual input
    }

    setSelectedYear(calculatedYear);
    setValue("yearRespectOfGranted", calculatedYear); // Update form value
  };

  // Dropdown options
  const yearOptions = [
    { label: "Arrears", value: "Arrears" },
    { label: `Year(-1) (${currentYear - 1})`, value: (currentYear - 1).toString() },
    { label: `Year(-2) (${currentYear - 2})`, value: (currentYear - 2).toString() },
    { label: `Year(-3) (${currentYear - 3})`, value: (currentYear - 3).toString() },
    { label: "Other", value: "other" },
  ];

  return (
    <div>
      {/* Dropdown for year selection */}
      <select
        className="w-full border p-2 rounded"
        onChange={handleYearChange}
        value={selectedYear}
      >
        <option value="">Select Year</option>
        {yearOptions.map((option) => (
          <option key={option.value} value={option.value}>
            {option.label}
          </option>
        ))}
      </select>

      {/* Show input field if "Other" is selected */}
      {selectedYear === "" && (
        <input
          type="number"
          placeholder="Enter Year"
          value={customYear}
          onChange={(e) => {
            setCustomYear(e.target.value);
            setValue("yearRespectOfGranted", e.target.value); // Update form value
          }}
          className="w-full border p-2 rounded mt-2"
        />
      )}
    </div>
  );
};

export default YearSelector;

```

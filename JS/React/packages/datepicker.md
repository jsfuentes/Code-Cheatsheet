# DatePicker

```jsx
import React from "react";
import PropTypes from "prop-types";
import { default as ReactDatePicker } from "react-datepicker";

DatePicker.propTypes = {
  selected: PropTypes.object,
  onChange: PropTypes.func,
  className: PropTypes.string,
  dateFormat: PropTypes.string,
  openToDate: PropTypes.object,
};

export default function DatePicker(props) {
  return (
    <ReactDatePicker
      showPopperArrow={false}
      //popperPlacement="top-start"
      todayButton="Today"
      // locale="en-US"
      minDate={new Date()}
      selected={props.selected}
      onChange={props.onChange}
      className={props.className}
      dateFormat={props.dateFormat}
      openToDate={props.openToDate}
    />
  );
}
```

```jsx
<DatePicker
  selected={startDateObject}
  onChange={(date) => setStartDateTime(date.toISOString())}
  dateFormat="EEE, do MMMM yyyy"
  className="w-64"
  />
```


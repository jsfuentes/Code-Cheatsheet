# [React-Select](https://github.com/JedWatson/react-select)

```bash
yarn add react-select
```

### Usage

```jsx
import React from 'react';
import Select from 'react-select';

const options = [
  { value: 'chocolate', label: 'Chocolate' },
  { value: 'strawberry', label: 'Strawberry' },
  { value: 'vanilla', label: 'Vanilla' },
];

class App extends React.Component {
  state = {
    selectedOption: null,
  };
  handleChange = selectedOption => {
    this.setState(
      { selectedOption },
      () => console.log(`Option selected:`, this.state.selectedOption)
    );
  };
  render() {
    const { selectedOption } = this.state;

    return (
      <Select
        value={selectedOption}
        onChange={this.handleChange}
        options={options}
      />
    );
  }
}
```

## Wrapper

```jsx
import React from "react";
import PropTypes from "prop-types";
import { default as ReactSelect } from "react-select";

export default function Select({ options, onChange, rightAlign, value }) {
  return (
    <ReactSelect
      value={value}
      className="react-select-container"
      classNamePrefix="react-select"
      options={options}
      defaultValue={options[0]}
      onChange={onChange}
      isSearchable={false}
      isRtl={rightAlign}
    />
  );
}

Select.propTypes = {
  options: PropTypes.array.isRequired,
  onChange: PropTypes.func,
  rightAlign: PropTypes.bool,
  value: PropTypes.any
};

Select.defaultProps = {
  rightAlign: false
};

```


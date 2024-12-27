# Telephone Input

[UI Discussion](https://uxmovement.com/forms/bad-practices-on-phone-number-form-fields/)

## React Package

## Installation

```
npm install react-phone-input-2 --save
```

## Usage

- has international code selection, validation, and autoformatting as you would want

```javascript
import PhoneInput from 'react-phone-input-2'
import 'react-phone-input-2/lib/style.css'
 
const [phone, setPhone] = useState("")
<PhoneInput
  country={'us'}
  value={phone}
  onChange={phone => setPhone(phone)}
/>
```


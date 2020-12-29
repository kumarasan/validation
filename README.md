# validation
validation

## Code Example

```
import React, { Fragment, useMemo, useReducer, useState } from 'react';
import Validator from '../index';

export function Example() {
  const validator = useMemo(() => new Validator(), []);
  const [, forceUpdate] = useReducer(x => x + 1, 0);
  const [state, setState] = useState({
    email: ""
  })

  const onChange = (event) => {
    const { name, value } = event.target;
    setState({
      ...state,
      [name]: value
    })
  }

  const onBlurValidation = (event) => {
    const { name, value } = event.target;
    setState({
      ...state,
      [name]: value
    })
    validator.showMessageFor(name)
  }


  const submitForm = () => {
    const { email } = state
    if (validator.allValid()) {
       // onsuccess
    } else {
      validator.showMessages();
      forceUpdate()
    }
  }

  const validatoremail = validator.message('email', email, 'required|email',
  { messages: { 'required': 'email address is required', 'email': 'Please enter a valid Email address' } })
  
  return (
    <Fragment>
        <input  
      type="text" 
      placeholder="Email" 
      onChange={onChange} 
      onBlur={onBlurValidation}
      value={email}
    />
    <p>{validatoremail}</p>
    </Fragment>
  )
}

export default Example```

# useRef

`특정 DOM`을 가져올 수 있도록 해주며, 렌더링과 관계 없는 변수를 선언할 때 사용합니다.<br/>
이번 파트는 useState에서 활용한 예제를 그대로 사용합니다.

## useRef 선언하기

```js
import React, { useState, useRef } from "react";
```

```js
import React, { useState, useRef } from "react";

function InputSample() {
  const [inputs, setInputs] = useState({
    name: "",
    nickname: "",
  });
  const nameInput = useRef();
  const { name, nickname } = inputs;

  const onChange = (e) => {
    const { name, value } = e.target;

    setInputs({ ...inputs, [name]: value });
  };

  const onReset = () => {
    setInputs({
      name: "",
      nickname: "",
    });
  };

  return (
    <div>
      <input name="name" placeholder="이름" onChange={onChange} value={name} />
      <input
        name="nickname"
        placeholder="닉네임"
        onChange={onChange}
        value={nickname}
      />
      <button onClick={onReset}>초기화</button>
      <div>
        <b>값:</b>
        {name} ({nickname})
      </div>
    </div>
  );
}

export default InputSample;
```

nameInput에 useRef 객체를 담습니다.

## useRef로 DOM 제어하기

```js
import React, { useState, useRef } from "react";

function InputSample() {
  const [inputs, setInputs] = useState({
    name: "",
    nickname: "",
  });
  const nameInput = useRef();
  const { name, nickname } = inputs;

  const onChange = (e) => {
    const { name, value } = e.target;

    setInputs({ ...inputs, [name]: value });
  };

  const onReset = () => {
    setInputs({
      name: "",
      nickname: "",
    });
    nameInput.current.focus();
  };

  return (
    <div>
      <input
        name="name"
        placeholder="이름"
        onChange={onChange}
        value={name}
        ref={nameInput}
      />
      <input
        name="nickname"
        placeholder="닉네임"
        onChange={onChange}
        value={nickname}
      />
      <button onClick={onReset}>초기화</button>
      <div>
        <b>값:</b>
        {name} ({nickname})
      </div>
    </div>
  );
}

export default InputSample;
```

해당 DOM을 반영하고 싶은 곳에 ref={변수명}을 넣고 예제에는 초기화를 누르면 focus 기능을 사용할 수 있도록 하였습니다.<br/>
useRef 객체가 담긴 변수는 current를 가지고 `current`를 활용하여 직접 DOM을 컨트롤 할 수 있게 됩니다.

## useRef로 컴포넌트 안의 변수 만들기

만약 컴포넌트에서 일반 변수를 선언하게 되면 컴포넌트가 렌더링 됐을 때 **초기화**가 됩니다.<br/>
때문에 굳이 `바꿀 필요가 없는 변수`가 필요할 때 사용합니다. 그래서 useRef로 변수를 선언하게 되면 **컴포넌트가 리렌더링 되지 않게** 됩니다.

```js
const nextId = useRef(4);
nextId.current; // 4
```

nextId에는 초기 4라는 값이 들어가고 current로 현재의 값을 가져올 수 있습니다.<br/>
이 4라는 값은 의도적으로 추가하지 않는 이상 계속 이 상태를 가지고 가며, **리렌더링 되지 않습니다.**

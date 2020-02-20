# ECMAScript

## Modules 정의
- 하나의 프로세스를 수행하는 단위 프로그램을 모듈이라고 합니다<br>
- 모듈은 더 이상 나누어지지 않는 최소 단위 프로그램입니다.<br>
- 자주 사용되는 코드를 별도의 파일로 만들어서 필요할 때마다 재활용할 수 있습니다.<br>

<br>
<br>

## Modules loader

export 와 import를 통하여 Modules를 내보낼 수 있고, 가져올 수 있습니다.<br>

<br>

### export 
함수, 객체, 원시 값을 내보낼 때 사용할 수 있습니다.

### export 내보내기

```js
// 하나씩 내보내기
export let name1, name2, …, nameN; // var, const도 동일
export let name1 = …, name2 = …, …, nameN; // var, const도 동일
export function functionName(){...}
export class ClassName {...}

// 목록으로 내보내기
export { name1, name2, …, nameN };

// 내보내면서 이름 바꾸기
export { variable1 as name1, variable2 as name2, …, nameN };

// 비구조화로 내보내기
export const { name1, name2: bar } = o;

// 기본 내보내기
export default expression;
export default function (…) { … } // also class, function*
export default function name1(…) { … } // also class, function*
export { name1 as default, … };

// 모듈 조합
export * from …; // does not set the default export
export * as name1 from …;
export { name1, name2, …, nameN } from …;
export { import1 as name1, import2 as name2, …, nameN } from …;
export { default } from …;

```

### import 
다른 모듈에서 내보낸 바인딩을 가져올 때 사용합니다.

### import 가져오기
```js

import defaultExport from "module-name";
import * as name from "module-name";
import { export1 } from "module-name";
import { export1 as alias1 } from "module-name";
import { export1 , export2 } from "module-name";
import { foo , bar } from "module-name/path/to/specific/un-exported/file";
import { export1 , export2 as alias2 , [...] } from "module-name";
import defaultExport, { export1 [ , [...] ] } from "module-name";
import defaultExport, * as name from "module-name";
import "module-name";
var promise = import("module-name");

```


## 참고
<a href="https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/export">https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/export</a><br>
<a href="https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/import">https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/import</a><br>

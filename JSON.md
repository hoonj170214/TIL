객체는 자바스크립트를 실행하는 시간에 메모리 상에서만 존재하는 구조이다. 그래서 데이터로서 주고받기 힘들다.

데이터로서 주고받는다는 의미란?

- 서버로부터 데이터를 받아야 할때
- 웹앱에서 서버로 데이터를 보내야 할때
- 데이터를 브라우저 상에서 어떤 저장장치에 저장해야 할때(로컬스토리지, 세션스토리지 , DB등)

→ 객체 자체를 저장할 수 없기 때문에 뭔가 방법이 필요하다.

⇒ 데이터를 교환하기 위한 포맷 JSON

JSON 은 자바스크립트 객체와 유사하게 생겼다.

JSON 문법
value 가 문자열일 경우 “” 로 감싸줘야 한다.
마지막 속성의 컴마 (꼬리 컴마 (tail comma) )는 빼야 한다.
JSON이 지원하는 value의 타입

- number
- string
- boolean
- 배열
- 객체
  → 자바스크립트 객체는 메서드를 사용할 수 있다. 하지만 JSON은 데이터이기 때문에, 함수(메서드)는 지원하지 않는다.

```
const jsonString = `	{
	"name": "jang seong hoon",
	"age": 26, 
	"bloodType": "O"
}`;
```

**문자열로 만들어진 JSON 데이터**를 자바스크립트에서 사용하기 위해서 **객체 형태**로 바꿔야 한다.

자바스크립트가 JSON 이라는 내장 객체를 제공한다. 이걸 써서 간단하게 바꿀 수 있다.

```
const myJson = JSON.parse(jsonString);

// 객체로 만들었으니 속성에 접근할 수 있다.
console.log(myJson.name); // jang seong hoon


```
객체 데이터를 전송하기 위해서 JSON 으로 만들고 싶다면?
stringify : 문자열화 한다
괄호 안에 객체를 넣어주면, 객체를 문자열화 한다는 뜻이다. 객체가 JSON으로 만들어진다.

```
console.log(JSON.stringify(myJson));

// {"name": "jang seong hoon", "age": 26, "bloodType": "O"}

```

이렇게 리턴된 문자열을 서버에 전송하거나 DB에 저장하면 된다.
꺼내올때는 다시 JSON.parse 로 꺼내와서 업데이트하고, 다시 JSON.stringify 으로 문자열로 만든다음 저장하면 된다.
만약 JSON 데이터를 업데이트 할 때, 오류가 난다면?
JSON.parse 코드 실행이 실패하고, 프로그램이 종료된다.
→ 사용자 경험에 안 좋다.
⇒ JSON.parse 할때 발생하는 오류는 예외로 발생하기 때문에 , try - catch 구문으로 잡을 수 있다.
✅
다시 말하면 JSON.parse 할때는 항상 try-catch 로 오류상황에 대비해야 한다.

```
try {

    const myJson = JSON.parse(jsonString);

    console.log(myJson.name);
    console.log(JSON.stringify(myJson));

} catch(e) {
console.log('다시 한번 시도해주세요');
}
```

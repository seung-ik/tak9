# jest mocking

테스트 하고자 하는 코드가 의존하는 부분을 가짜로(mockdata)로 대체하는 기법을 mocking 이라고 한다. 실제데이터를 가공하고 롤백하는 과정들 database 를 건드리는 작업은 테스트작업에 부담이 될수 있다.
jest 는 타 라이브러리의 지원없이 mocking을 구현할수있는 장점이 있다.

## jest.fn() 사용법

```js
//가짜 함수를 생성할수있다.
const mockFn = jest.fn();

//인자를 넘겨 사용할수 있다.
mockFn('adsb')
mockFn([1,2],4)

mockFn.mockReturnValue("will return value"); // 함수의 리턴값을 미리지정할수있다.
mockFn.mockResolvedValue("will resolvedValue"); // 비동기 함수의 resolve 될 값도 미리 지정 할수 있다.

mockFn.mockImplementation((name) => `my name is ${name}`); // 구현 코드를 직접 만들수도 있다. 주로 사용되지 않을까 싶다.
console.log(mockFn('tmdddlr')) // my name is tmddlr

// mockImplementation 이 주로 쓰이고 mockImplementationOnce 도 많이 쓰이네 mockImplementationOnce 는 뭐지? 
// 1회용 한번쓰면 증발하는 함수

const spyFn = jest.spyOn(calculator,'add'); // jest.spyOn(object, methodName)
const result = calculator.add(2,3);

expect(spyFn).toBeCalledTimes(1); // mockfunc 는 실행횟수를 기억할수있다.
expect(spyFn).toBeCalledWith(2,3) // mockfunc 는 들어온 인자를 기억할수있다.
```

## 테스트 코드의 작성
```js
test("테스트 설명", () => {
  expect('검증대상').toBe('기대 결과');
});
```
toXXX 부분에서 사용되는 함수를 testMatcher라고 한다
toBe() 함수는 primitive한 값을 비교할때 사용된다.
toEqual() 함수는 객체값을 비교
toContain() 특정 원소가 배열에 들어있는지 테스트
toThrow() 에러테스트(작성시 주의사항있음) 

```js
test("array",()=>{
  const color = [1,2,3];
  expect(color).toContain('yellow');
  expect(color).not.toContain(4);
})
```

연관된 test() 를 describe를 통해 그룹화 해줄수 있다.
```js
describe("group1",() => {
  test("test 1-1",() => { }) // test 대신 it 을 사용해도 된다(차이점 없음)
  test("test 1-2",() => { })
  test("test 1-3",() => { })
}) 
```

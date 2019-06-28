# struct + typedef

</br>

## 문제

``` C
typedef struct stack {
    ...
} stack;
```

C에서 구조체 선언 시, 위 stack처럼 이름을 두 번 선언하는 경우가 있다. 저 'stack' 들의 의 차이점은 무엇이고 어떻게 써야 옳은 걸까?  

struct를 선언하는 형태가 많은데, 개념이 좀 헷갈려서 정리해본다. 초심으로 살펴보고, 어떻게 써야 좋을 지 다시 생각해보자. 🌱  

그를 위해서 명확히 가져가야할 3가지인 : (1) struct definition, (2) struct declaration, (3) typedef에 관하여 설명하겠다.  

</br>

## 기본 개념 정리

</br>

### (1) struct definition

먼저, struct는 아래와 같이 정의하여 만들 수 있다.

``` C 
// Shoe 타입 정의
struct Shoe {
   ...
};
```

이건 `struct Shoe` 이라는 새로운 type을 정의해준 것과 같으므로, 아래처럼 표현할 수 있다. 

### (2) struct declaration

``` C
// Shoe 타입의 airmax 변수 선언
struct Shoe airmax;
```

그럼 이건 `struct Shoe` 이라는 type을 지닌 `airmax` variable이 된다. // airmax라는 이름의 신발 타입

### + (1) + (2) struct definition & declaration

``` C
// Shoe 타입 정의 및 airmax 변수 선언
struct Shoe {
   ...
} airmax;
```

그리고 이걸 한방에 쓰면 이렇게.. 그러니 여기서 주의할 점은, `airmax` 는 결코 `struct Shoe` 와 같은 아이가 아니라는 것. 즉, 우리는 `struct Shoe cortez;` 또한 추가적으로 만들 수 있다는 말이다. 

### (3) typedef

``` C
typedef OldTypeName NewTypeName;
```

`typedef` 는 알다시피 한 type에 새로운 이름을 붙이는 것이고, 이를 struct에 적용하면 아래처럼 된다.

``` C
// Nike 타입 정의 (Shoe와 같음)
typedef struct Shoe Nike;

// Adidas 타입 정의
typedef struct {
   ...
} Adidas;
```

즉, `struct Shoe` 는 이제 `Nike` 라고 쓸 수 있당. 그러니 선언하듯 아래와 같은 코드 가능하다.

``` C
// Shoe 타입의 airmax97 변수 선언
struct Shoe airmax98;
// Nike 타입의 airmax98 변수 선언 (struct Shoe 타입과 같음)
typedef struct Shoe Nike;
Nike airmax97;
```

</br>

## 활용

그렇다면, 어떻게 struct를 활용하면 좋을까? 내가 자주 하던 실수는 아래와 같다.

``` C
typedef struct Shoe {
   ...
} Nike;
```

`struct Shoe` 는 정의되지만, 바로 Nike라는 이름이 붙여진다. 내가 만약 오로지 Nike 신발만 신는 사람이라서, `Shoe` 라는 type을 따로 쓸 필요를 못느낀다면 굳이 이름을 쓸 필요가 없을 것이다.  

불필요한 코드는 제거해주는게.. 프로그래머의 미덕ㅎㅎ이니까. 예시로 든 Shoe와 Nike가 조금 애매모호한감은 있지만, 그래도 누군가 읽는다면.. 내가 전달하고 싶은 내용은 이해했으리라고 믿는다. 혹시 틀린게 있다면 꼭! 말씀해주시길   

그러니, 필요에 따라서 아래처럼 이해한 내용을 바탕으로 알맞게 활용해서 같이 쓰면 될 것이다.

``` C
struct Shoe {
   ...
}; // Shoe type 정의
typedef struct Shoe Nike; // alias
Nike airmax97; 
```

``` C
typedef struct {
   ...
} Nike; // Nike type 정의
Nike airmax98;
```

</br>

## References

[[Stackoverflow] C : typedef struct name {…}; VS typedef struct{…} name;](https://stackoverflow.com/questions/17720223/c-typedef-struct-name-vs-typedef-struct-name)
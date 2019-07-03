# Refactoring : Replace Enum with Polymorphism.

[스위프트로 다시보는 객체지향 프로그래밍: 피해야할 코딩 습관](https://soojin.ro/blog/solid-principles-in-swift)

[Refactoring: Replace Enum with Polymorphism](https://medium.com/swift-fox/refactoring-replace-enum-with-polymorphism-c4803baeba07)

</br>



## Open Closed Priciple

SOLID 법칙 중 하나인, 'O'에 해당하는 'Open Closed Priciple'이다. 기능 추가나 변경에는 Open되어 있어야 하고, 이 과정에서 해당 코드의 모듈들은 Closed된 상태여야 한다는 말이다. 

</br>



## Problem

``` Swift
enum Animal {
    
    enum Size {
        case small
        case medium
        case large
    }
    
    case dog
    case cat
    case cow
    
    var noise: String {
        switch self {
        case .dog:
            return "woof"
        case .cat:
            return "meow"
        case .cow:
            return "moo"
        }
    }
    
    var size: Size {
        switch self {
        case .dog:
            return .medium
        case .cat:
            return .small
        case .cow:
            return .large
        }
    }
    
}
```

이런 코드가 있다고 치자. 만약에 case문을 추가하려고 보면, 기존에 쓰이던 모듈을 건드리지 않고(Open 'Closed' Principle)는 불가능해진다. 이보다 더 많은 분기가 있다고 생각하면 정말 수도 없을 것…

</br>



## Solution

``` Swift
enum AnimalSize {
    case small
    case medium
    case large
}

protocol Animal {
    var noise: String { get }
    var size: AnimalSize { get }
}

struct Dog: Animal {
    var noise = "woof"
    var size = AnimalSize.medium
}

struct Cat: Animal {
    var noise = "meow"
    var size = AnimalSize.small
}

struct Cow: Animal {
    var noise = "moo"
    var size = AnimalSize.large
}
```

그리고 이를 해결하기 위한.. 내가 사랑하는 프로토콜! enum + protocol + 다형성을 이용했다. 이제 case 추가 시, 기존 코드를 크게 건드리지 않고 쉬운 확장이 가능하다!
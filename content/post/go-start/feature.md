+++
authors = ["Sangbae Yun"]
categories = ["How-to"]
date = "2016-09-03T13:10:03+09:00"
draft = true 
tags = ["geginning"]
title = "Go의 주요 특징들"
toc = false
+++

## 단순함
Go 언어는 단순함(simplicity)과 실용성(pragmatism)을 지향하는 언어로 이 두가지 철학이 다른 모든 것들 보다 상위에 있다. go 언어에 없는 것들을 보자. 
  
 * 패턴매칭 
 * 함수 프로그래밍 : 어느 정도 특징을 가지고 있기는 하지만 지향점은 아니다.
 * immutable variables 
 * Option types : 값외에 유효한지, 초기화가 됐는지 등의 추가적인 정보를 설정할 수 있다. 
 * 예외(exception)가 없다.
 * 클래스도 없다. 
 * 제너릭(jeneric)를 지원하지도 않는다.

현대적인 언어들이라면 당연히 가지고 있음직한 굵직한 특성들을 가지고 있지 않다. 심지어 "Go는 40년 동안의 프로그래밍 언어에 대한 연구를 던져버린 유일한 언어"라고 평가를 받기도 한다(제너릭의 경우 지원하려는 움직임이 있는 것 같기는 하다). 그리고 이러한 철학을 그대로 하고 있는데, 1.0 버전이 나온 이후 1.7 까지 문법적인 변화가 거의 없다. 

1.0 이 나온게 2012년이니 5년 동안 변한게 없다는 이야기다. 따라서 개발자는 호환성 문제에서 자유로우며, 기술에 대한 숙련도를 꾸준히 유지 할 수 있다. 단순함을 포기하지 않기 때문에 가능한 일이다. [Go release History](https://golang.org/doc/devel/release.html)에서 버전별 변경점을 찾아 볼 수 있는데, 버그 수정, 지원 플랫폼, 툴 추가, 컴파일러 변경, 가비지 컬랙터 효율화 등 언어 내적인 것들이 대부분이다.

계속 단순함을 유지하면서, 언어적인 발전이 가능 할 것인지에 대한 의구심을 가질 수 있다. 이렇게 생각해보자. 복싱은 주먹을 사용하는 격투기 중 최고로 평가받고 있다. 그런데 복싱이 가지고 있는 기술이라는게 스트레이트, 잽, 어퍼, 훅 4가지 밖에 없다. 기술이 적기 때문에 시작하기가 쉽고 반복훈련을 통해서 빠르게 기량을 높일 수 있다. 그리고 직관적인 만큼 실전에서의 응용이 용이하다. 

Go 언어도 마찬가지다. 1-2주면 언어의 거의 모든 기능에 익숙해질 수 있으며, 반복 훈련을 통해서 빠르게 기량을 높일 수 있다. 코드가 직관적이기 때문에 코드를 만들고 읽는게 쉬우며 그만큼 실전에 빠르게 써먹을 수 있다.

물론 언어의 단순함이 모든 경우에 장점이 될 수는 없을 것이다. Go 언어는 시스템, 네트워크 프로그램 특히 클라우드 환경에서 작동하는 프로그램의 개발에는 강력한 면모를 보여주지만 모바일, 데스크탑 애플리케이션에도 강점을 보여줄지는 의문이다(애초에 이쪽은 별로 신경을 쓰고 있지 않기 때문에 판단하기는 애매모호하긴 하다). 

## 클라우드와 친한 go 언어
단순함과 이로부터 파생되는 특징은 클라우드 환경에 잘 맞는 경향이 있다. 분산환경은 시스템이 분산된다는 의미외에 소프트웨어가 분산된다는 의미도 있다. 이런 환경에서는 소프트웨어들이 많은 기능을 가지고 있을 필요가 없다. 필수적인 기능만 가진 여러 소프트웨어들이 서로 데이터를 주고 받는 식으로 작동을 하는게 더 효율적이다. 이런 소프트웨어 운영 모델은 리눅스에서 찾아볼 수 있다.    
```sh
# ps aux | grep chorm | grep -v grep | awk '{print $2}' | xargs kill 
```
ps로 프로세스 목록을 출력하면 grep으로 chrom 프로세스의 정보만 가져오고, awk를 이용해서 **PID**를 읽어서 kill로 죽이는 일을 하는 스크립트다. 클라우드환경에서 뜨는 **MSA**(go언어를 이용한 MSA 문서를 만들어봐야 겠다.)가 이런 방식으로 작동한다.

클라우드는 컴퓨터와 네트워크, 운영체제를 하나로 통합한다. 이런 환경에서 프로그래밍 언어의 버전, 라이브러리 의존성을 신경쓰면서 애플리케이션을 배포하는 건 굉장히 어려운 일이다. 최근 도커(docker)가 핫한 것도 운영체제 등 주변환경이 어떻든지 간에 자유롭게 배포 할 수 있고, 동일하게 작동 할 것을 보장해 주기 때문이다. 

Go 언어로도 이런 개발 & 배포 환경을 만들 수 있다. 도커와 함께 클라우드를 위한 컨테이너 솔류션을 만들고 싶다면 Go는 최고의 선택이 될 것이다.

## struct 와 객체지향
Go는 클래스(class) 키워드를 가지고 있지 않다. 21 세기에 클래스 키워드를 지원하지 않는 언어라니 놀랍다. 그렇다고 해서 객체지향 프로그래밍을 포기해야 한다는 얘기는 아니다. Go는 지금은 C 언어에서나 볼 수 있는 **struct** 키워드를 제공하며, 이 것을 이용해서 객체지향 프로그램을 만들 수 있다. 

struct는 하나이 상의 필드들로 구성된 데이터 타입으로 레코드 형식의 데이터 그룹을 만들기 위해서 사용한다. 개인 정보를 다루는 애플리케이션을 개발한다면 아래와 같은 **person** 스트럭처를 만들 수 있을 것이다. 
```go
type person struct {
    name string
    age  int
}
```

## 에러 처리

## 인터페이스
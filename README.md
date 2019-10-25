# 아트위크 ARTWEEK 

![Artweeklogo](images/Artweeklogo.png)

<center>"Artweek과 함께하는 예술적인 일주일"</center>

<p align="center">
  <img src="http://img.shields.io/:license-mit-green.svg"/>
  <img src="https://img.shields.io/badge/platform-bixby-blue.svg"/>
  <img src="https://img.shields.io/badge/language-javascript-brightgreen.svg"/>
</p>



Artweek 팀은 사용자가 오프라인 문화생활을 더욱 편리하게 즐길 수 있도록 영감을 제공합니다.



이용 중 문의사항이 있으신 경우 하기 e-mail 로 연락바랍니다.

:e-mail: makeartweek@google.com

## 목차

1. [아트위크란?](#아트위크란?)

2. [캡슐구조](#캡슐구조)

3. [캡슐설정](#캡슐설정)

4. [사전(Vocabulary)](#사전(Vocabulary))

5. [발화(Training)](#발화(Training))

6. [UI&UX(Layout)](#UI&UX(Layout))

8. [AWS 서버와 외부 DB](#)

11. [부록](#부록)

    


## 아트위크란?

> 아트위크 캡슐을 통해 오프라인 문화생활 정보를 확인할 수 있습니다. 오프라인  문화생활 정보를 아트위크 캡슐이 대신 찾아줍니다. 



## 캡슐구조

### models
> 파일구조
```cmd
├── actions
│   ├── GetCurrentPosition.model.bxb
│   ├── SearchByLocation.model.bxb
│   └── SearchEvent.model.bxb
└── concepts
   ├── Primitive
   │   ├── Event
   │   │   ├── Concert.model.bxb
   │   │   ├── Director.model.bxb
   │   │   ├── EventID.model.bxb
   │   │   ├── EventStatus.model.bxb
   │   │   ├── Exhibition.model.bxb
   │   │   ├── Fee.model.bxb
   │   │   ├── Images.model.bxb
   │   │   ├── ImgUrl.model.bxb
   │   │   ├── Musical.model.bxb
   │   │   ├── Performer.model.bxb
   │   │   ├── Theater.model.bxb
   │   │   ├── TimeTable.model.bxb
   │   │   ├── Title.model.bxb
   │   │   ├── Type.model.bxb
   │   │   └── TypicalAgeRange.model.bxb
   │   ├── Place
   │   │   ├── Address.model.bxb
   │   │   ├── District.model.bxb
   │   │   ├── Location.model.bxb
   │   │   ├── LocationID.model.bxb
   │   │   ├── Near.model.bxb
   │   │   └── Nearby.model.bxb
   │   ├── Signal
   │   │   ├── DirectorPostposition.model.bxb
   │   │   ├── PerformerPostposition.model.bxb
   │   │   └── SearchKeyword.model.bxb
   │   └── Time
   │       ├── CreatedAt.model.bxb
   │       ├── EndDate.model.bxb
   │       ├── Recent.model.bxb
   │       └── StartDate.model.bxb
   └── Structure
       ├── InfoSearchState.model.bxb
       ├── MyPositionList.model.bxb
       ├── Mypos.model.bxb
       ├── NearSearchState.model.bxb
       ├── OnClick.model.bxb
       └── Point.model.bxb
```



> `actions`폴더에는 ? 병합 후 작성

`concepts`폴더는 `Primitive`와 `Structure` 두 폴더로 나누어 구성하였습니다.

`Primitive`폴더에는 `Structure`에 해당하는 `Event`, `Place`, `Time`, `signal`들을 생성하여 관리함으로써 structure concept와 primitive concept의 구분을 명확히 하였습니다. 

### resources

> 파일구조


```cmd
├── base
│   ├── capsule.properties
│   ├── endpoints.bxb
│   ├── layouts
│   │   └── macros
│   │       ├── EventOneImage.layout.bxb
│   │       ├── EventSummary.layout.bxb
│   │       ├── LocDetail.layout.bxb
│   │       └── LocEvent.layout.bxb
│   └── views
│       ├── InfoSearchState.view.bxb
│       └── NearSearchState.view.bxb
└── ko-KR
   ├── artweek.hints.bxb
   ├── capsule-info.bxb
   ├── dialogs
   │   ├── NearSearchResult.dialog.bxb
   │   └── Result.dialog.bxb
   └── vocab
       ├── Concert.vocab.bxb
       ├── DirectorPostposition.vocab.bxb
       ├── District.vocab.bxb
       ├── Exhibition.vocab.bxb
       ├── Musical.vocab.bxb
       ├── Nearby.vocab.bxb
       ├── PerformerPostposition.vocab.bxb
       ├── Recent.vocab.bxb
       ├── SearchKeyword.vocab.bxb
       ├── Theater.vocab.bxb
       └── Type.vocab.bxb
```




## 캡슐설정

`hints`

```js
hints {
uncategorized {
  hint (아트위크에서, 강남역에서 가까운 전시 보여줘)
  hint (아트위크에서, 아이유 콘서트 정보 좀 찾아줘)
  hint (아트위크에서, 송광일 나오는 연극 알려줘)
  hint (아트위크에서, 주변에 뭐 있어?)
  hint (아트위크에서, 내 근처에서 하는 콘서트 알려줘)
  hint (아트위크에서, 연말에 하는 공연 좀 알려줄 수 있어?)
  hint (아트위크에서, 뮤지컬 맘마미아 보여줘)
  hint (아트위크에서, 주변에서 하는 연극 뭐 있어?)
}
}
```



## 사전(Vocabulary)

아트위크 캡슐이 다양한 패턴의 발화를 인식할 수 있도록 여러 property에 대한 `vocab` 파일을 생성하여, 대표어에 대해서 최대한 많은 동의어를 구축함으로써 최대한 다양한 발화에 적절한 정보를 제공할 수 있도록 학습시킬 수 있습니다.

이러한 사전의 사용은 다음과 같은  `enum`, `name`, `text` 세 가지 타입을 적절히 사용하여야 하고, 이를 통해 빅스비가 사용자의 의도를 잘 알아들을 수 있습니다.



> [enum](https://bixbydevelopers.com/dev/docs/dev-guide/developers/training.vocabulary#top)

`vocab `중에 `District`의 경우  `enum`을 사용하였는데, 바뀔 가능성이 적은 데이터이므로 대표어인 지역에 해당하는 유의어와 더불어 `랜드마크` 및 `지하철 역명`을 추가하였습니다. 이를 통해 다양한 발화에 대해 정해진 대표어로 인식하게 함으로써 위치 주소를 명확하게 인식할 수 있게 하였습니다.

```js
vocab (District){

  "강남구" {

    "강남구",
    "강남",
    "강남역",
    "역삼역",
    "코엑스",
  }
   ...
}

```



> [name](https://bixbydevelopers.com/dev/docs/dev-guide/developers/training.vocabulary)

`SearchKeyword`의 경우 `name` 을 사용하였습니다. 사용자에 따라 가장 다양하게 발화가 될 동사라고 생각되어 `검색`이라는 의도를 나타낼 수 있는 비슷한 동사를 추가하였습니다. 여러 다양한 발화에 대한 패턴학습을 통해 이후 `vocab` 에 들어있지 않더라도 자동으로 `SearchKeyword` 로 인식하게 됩니다.

```js
vocab(SearchKeyword) {
  // 보편적인 검색키워드  
  "검색",
  "검색해",
  "검색해줘",
  "검색해라",
  "검색해주세요",
  "검색해줘요",
  "검색좀",
}
```




## 발화(Training)

**사용자 현재 위치 중심으로 검색하기** 
사용자 질의:
근처에서 하는 연극 알려줘 

정보 제공:
‘사용자의 현재 위치’에서 5킬로 내에 하는 연극 정보 제공

**특정 장소 중심으로 검색하기**
사용자 질의:
강남역/강남 근처에서 하는 전시 알려줘 

정보 제공:
‘강남역/강남의 중심에서 5킬로 내에 하는 전시 정보 제공

**특정 일정을 중심으로 검색하기**
사용자 질의:
이번 주/이번 달/오늘 하는 콘서트 알려줘

정보 제공:
‘특정 일정’에 해당하는 콘서트 정보 제공

**특정 타입을 중심으로 검색하기**
사용자 질의:
콘서트/연극/뮤지컬/전시 알려줘

정보 제공:
‘특정 타입’에 해당하는 정보 제공

**행사 제목을 중심으로 검색하기**
사용자 질의:
헤드윅 뮤지컬 정보 알려줘

정보 제공:
‘행사 제목’에 해당하는 정보 제공



## UI&UX(Layout)

빅스비를 개발할 때 layout 부분이 다소 생소하게 느껴질 수 있지만, 참고자료를 잘 활용해보시면 직접 디자인을 하지 않아도 빅스비에 이미 구현된 template를 사용할 수 있어서 쉽게 view를 구현하실 수 있습니다. 

Layout은 총 view와 view에서 사용 가능한 macro로 구성되어있습니다.

### View

view는 `InfoSearchState` 와 `NearsearchState` 를 사용하였습니다.


### Macro

view의 효율성을 위해서 macro로 `EventOneImage`, `EventSummary`, `LocDetail`, `LocEvent` 를 사용하였습니다.




![UIUXview](images/UIUXview.png)

2개 이상의 정보를 가지고 올 때는 `EventSummary` 가 사용되며, 사용자가 의도를 가지고 상세정보를 원할 때는 `EventOneImage` 가 사용됩니다.

1개의 정보를 가지고 올 때는 `EventOneImage` 로 사용자에게 view를 전달하여 상세정보를 보여주게 됩니다. 

`macro`를  잘 활용하시면 사용자의 다양한 발화에 따라 `view`를 재사용할 수 있어서 layout 개발할 때 효율적입니다.




## AWS 서버와 외부 DB

### Flow

![flowDiagram](images/flowDiagram.png)



### 외부 DB

빅스비 스튜디오에는 내부 DB를 제공하지 않았기 때문에 아트위크 팀은 AWS Server를 통해 외부 DB를 구축하였습니다. 

처음에는 단순히 하나의 오픈 API를 사용하여 Business logic에서 구현하고자 했지만 아트위크가 제공하는 서비스는 최대한 많은 오프라인 문화생활(연극, 뮤지컬, 전시, 오페라, 클래식, 콘서트) 정보를 사용자에게 제공하고자 했기 때문에 다양한 오픈 API에서 제공하는 데이터를 보유하고자 했습니다.

그래서 input value에 따라 공연 종류를 구분하여 API를 선택해 정보를 구해오는 비효율적인 방법보다 원하는 모든 공연 정보를 미리 외부 DB에 저장하여 통합적으로 관리하는 필요성을 느꼈습니다.



### AWS server

AWS RDS,  Mysql을 사용하여 외부 DB 관리의 효율성을 높였고,

AWS에서 제공하는 API Gateway와 Lambda 함수를 이용하여 DB에서 정보를 제공할 수 있는 **아트위크만의 API**를 제작하였습니다.



### DB 최적화

![ERD](images/ERD.png)



아트위크의 DB는 하기 사진과 같이 1:N의 관계로 구성되어있습니다. 즉, 6개의 Event type과 이를 연결하는 1개의 Main location이 존재합니다.

공연 종류에 따라서 Table을 나누어서 원하는 종류의 공연이 아닌 타 종류의 공연은 검색대상에서 제외함으로써 검색속도를 증가시켰습니다.




## 부록

![Artweeklogo2](images/Artweeklogo2.png)

"from `Artweek` import `inspiration`"

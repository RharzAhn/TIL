앱바



코디네이터 레이아웃 - 뷰끼리 상호작용 작용하기

스크롤연동하기 - 뷰끼리 상호작용할때 사용, 뷰에서 발생한 스크롤정보를 코디네이터 레이아웃이 받아서 다른 뷰에 전달

코디네이터 레이아웃에 중첩 스크롤 뷰(NestedScrollView)를 포함하고 여기에 텍스트 뷰나 이미지 뷰를 넣으면 해당 뷰에서 발생하는 스크롤 정보를 코디네이터 레이아웃에 전달(layout_behavior)

*월,화 수업내용파일 요청하기



컬랩싱 툴바 레이아웃 - 앱바 접히는 형태 설정하기

컬랩싱 툴바 레이아웃(CollapsingToolbalLayout)은 앱바 레이아웃 하위에 선언하여 앱바가 접힐 때 다양한 설정을 할 수 있는 뷰

title 속성으로 앱바의 제목을 설정 - 제목을 설정하며 표기되게 할수있음

expandedTitleMarginStart, expandedTitleMarginBottom 속성으로 앱바가 접히지 않았을때 제목의 위치를 선정

내용이 정상으로 출력되지 못하는 상황이라면 contentScrim속성에 지정한 색상으로 앱바를 출력



스크롤 설정하기

앱바가 스크롤될지를 설정하는 layout_scroll Flags

scroll|enterAlways:스크롤시 ~~~



탭 레이아웃 - 탭 버튼 구성

탭 레이아웃은 탭tab으로 구분하는 화면에서 탭 버튼을 배치하는 레이아웃

xml, active.kt파일 둘다에서 탭 구성가능?



```kotlin
app:tabMode="scrollable" -> 탭이 많을때 옆으로 넘겨가며 볼수있는거
```

```kotlin
app:tabGravity="start" -> 이거랑 스트롤러블 해주면 왼쪽부터 시작
```


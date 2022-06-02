## 익명 소셜 서비스 앱(AndTest1)

모든 화면에서 ui가 반복되는 형태 - RecyclerView 가 효율적으로 표현

리스트화면은 세로 RecyclerView, 글쓰기화면은 가로 RecyclerView 사용



#### 화면설계

화면설계서 작성하는게 좋음

각각화면이 별도로 전체 화면을 차지하고 있으면 Activity 사용이 편함

댓글쓰기,글쓰기처럼 화면이 유사한것들은 같은Activity에 조건에따라 타이틀만 변경



#### 메인화면

우측아래에 화면과 상관없이 떠있는 버튼 -> FloatingActionButton - Material 디자인 에 자주씀

ActionBar의 경우 테마로 지정ㅇ가능



##### 의존성추가

*build.gradle - dependencies 안에 작성

```kotlin
//이미지 로딩 라이브러리
api 'com.squareup.picasso:2.71828'
//시간 관련 라이브러리
implementation 'net.danlew:android.joda:2.10.2'
//파이어베이스(의존성 추가)
implementation 'com.google.firebase:firebase-core:15.0.0'
implementation 'com.google.firebase:firebase-database:15.0.0'
```



##### 이미지 다운

http://goo.gl/XAV537 에서 다운로드후 app/res/drawable 에 넣기



#### 메인화면

###### 메인화면 레이아웃(activity_main.xml)

```kotlin
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/recyclerView"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <com.google.android.material.floatingactionbutton.FloatingActionButton
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/floatingActionButton"
        android:layout_marginEnd="16dp"
        android:layout_marginRight="16dp"
        android:layout_marginBottom="16dp"
        android:clickable="true"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:srcCompat="@android:drawable/ic_dialog_email"/>
</androidx.constraintlayout.widget.ConstraintLayout>
```



*투명도가 들어간 배경을 사용하는 이유 : 배경 이미지의 컬러와 상관없이 텍스트가 잘보이도록 하기위해



#### 메인화면 카드

###### 메인화면 카드 레이아웃(activity_main.xml)

```kotlin
<?xml version="1.0" encoding="utf-8"?>
<androidx.cardview.widget.CardView xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/cardView"
    android:layout_width="match_parent"
    android:layout_height="220dp"
    app:cardCornerRadius="4dp"
    app:cardUseCompatPadding="true">

    <androidx.constraintlayout.widget.ConstraintLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <ImageView
            android:id="@+id/imageView"
            android:layout_width="0dp"
            android:layout_height="0dp"
            android:scaleType="centerCrop"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent"
            app:srcCompat="@drawable/default_bg" />

        <TextView
            android:id="@+id/contentsText"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginStart="32dp"
            android:layout_marginLeft="32dp"
            android:layout_marginTop="32dp"
            android:layout_marginRight="32dp"
            android:layout_marginBottom="32dp"
            android:background="#66000000"
            android:ellipsize="end"
            android:maxLines="2"
            android:padding="8dp"
            android:text="TextView"
            android:textColor="@color/white"
            android:textSize="24sp"
            app:layout_constrainedHeight="true"
            app:layout_constrainedWidth="true"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent" />

        <androidx.constraintlayout.widget.Guideline
            android:id="@+id/guideline1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:orientation="horizontal"
            app:layout_constraintGuide_percent="0.8" />

        <View
            android:id="@+id/bottomBackground"
            android:layout_width="0dp"
            android:layout_height="0dp"
            android:background="#77000000"
            app:layout_constraintBottom_toBottomOf="@+id/imageView"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="@+id/guideline1" />

        <ImageView
            android:id="@+id/clockImage"
            android:layout_width="wrap_content"
            android:layout_height="0dp"
            android:layout_marginStart="8dp"
            android:layout_marginLeft="8dp"
            android:layout_marginTop="8dp"
            android:layout_marginBottom="8dp"
            android:adjustViewBounds="true"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="@+id/guideline1"
            app:layout_constraintVertical_bias="0.0"
            app:srcCompat="@drawable/clock" />

        <TextView
            android:id="@+id/timeTextView"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginStart="8dp"
            android:layout_marginLeft="8dp"
            android:layout_marginTop="8dp"
            android:layout_marginBottom="8dp"
            android:text="TextView"
            android:textColor="@color/white"
            app:layout_constraintBottom_toBottomOf="@id/clockImage"
            app:layout_constraintStart_toEndOf="@id/clockImage"
            app:layout_constraintTop_toTopOf="@id/clockImage" />

        <TextView
            android:id="@+id/commentCountText"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginEnd="8dp"
            android:layout_marginRight="8dp"
            android:layout_marginTop="8dp"
            android:layout_marginBottom="8dp"
            android:text="TextView"
            android:textColor="@color/white"
            app:layout_constraintBottom_toBottomOf="@id/clockImage"
            app:layout_constraintEnd_toEndOf="@id/bottomBackground"
            app:layout_constraintTop_toTopOf="@id/clockImage" />

        <ImageView
            android:id="@+id/commentImage"
            android:layout_width="wrap_content"
            android:layout_height="0dp"
            android:layout_marginEnd="8dp"
            android:layout_marginRight="8dp"
            android:adjustViewBounds="true"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintEnd_toStartOf="parent"
            app:layout_constraintTop_toTopOf="@+id/guideline1"
            app:srcCompat="@drawable/comment" />

    </androidx.constraintlayout.widget.ConstraintLayout>
</androidx.cardview.widget.CardView>
```



#### 테마 및 컬러 지정

###### colors.xml에 다음코드 추가(resources 안에)

```kotlin
<!--    앱의 주요 색상-->
    <color name="colorPrimary">#2196F3</color>
<!--    앱의 어두운 부분 주요 색상-->
    <color name="colorPrimaryDark">#1976D2</color>
<!--    포인트 컬러-->
    <color name="colorAccent">#FF5722</color>
<!--    버튼에서 사용할 컬러-->
    <color name="colorButton">#2196F3</color>
<!--    버튼 텍스트에서 사용할 컬러-->
    <color name="colorButtonText">#FFFFFF</color>
```

###### styles.xml 생성후 작성

```kotlin
<?xml version="1.0" encoding="utf-8"?>
<resources>
<!--    Base application theme.-->
    <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
<!--        테마의 주요 컬러-->
        <item name="colorPrimary">@color/colorPrimary</item>
<!--        테마의 어두운 주요 컬러-->
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
<!--        테마의 포인트 컬러-->
        <item name="colorAccent">@color/colorAccent</item>
<!--        버튼의 컬러-->
        <item name="colorButtonNormal">@color/colorButton</item>
<!--        버튼등 텍스트 컬러-->
        <item name="android:textColor">@android:color/white</item>
    </style>
</resources>
```




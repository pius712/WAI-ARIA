# 짐싸 WAI-ARIA 가이드라인

## 1. Why ARIA?

Accessible Rich Internet Applications (ARIA)는 장애를 가진 사용자가 웹 컨텐츠, 웹 어플리케이션을 더욱 편리하게 사용 할 수 있게 해주는 어트리뷰트 집합(set of attributes)이다. ARIA를 사용하여 동적인 컨텐츠를 보조 기기(assistive technologies)에서도 경험 할 수 있도록 페이지 구조에 정보를 추가 할 수 있다.

---

## 2. ARIA

### Role

```jsx
<li role="menuitem">Open file...</li>
```

`role` 속성을 사용하여 보조 기기에 해당 요소가 어떻게 다루어져야하는 지 정보를 제공한다. 

[자주 사용되는 role](%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/%E1%84%8C%E1%85%A1%E1%84%8C%E1%85%AE%20%E1%84%89%E1%85%A1%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%83%E1%85%AC%E1%84%82%E1%85%B3%E1%86%AB%20role%20f009adc016e94d1f828cef460a60a125.csv)

### States and Properties

- [aria-label](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_aria-label_attribute)

     스크린 상에서 해당 element에 제공되지 않는 정보를 주기 위해서 사용. 

    ```html
    <button aria-label="팝업 닫기" onClick={handleClick}>X</button> 
    ```

- [**aria-labelledby**](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_aria-labelledby_attribute)

    `aria-labelledby` 는  DOM 객체(Element)에 대한 **핵심적인 설명** 을 전달해주는 역할을 한다.

    aria-label은 string으로 직접 설명해주는 것과 달리, `aria-labelledby`는 이를 설명해주는 라벨과 연결해주는 역할을 해준다.

    input 과  label 을  for / id 를 연결 시키는 것과 비슷하다.

    ```html
    <section
      aria-labelledby='cost'>
        <h2 id='cost'>견적가</h2>
        <p>
          ${cost}<span>원</span>
        </p>
    </section>
    ```

    ![%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/_2021-04-15__4.07.12.png](%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/_2021-04-15__4.07.12.png)

- [**aria-describedby**](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_aria-describedby_attribute)

     `aria-describedby` 는 DOM 객체를 설명하기 위한 것으로 일반적으로 **부가적인 설명**이 필요한 경우에 사용한다.

     웹 어플리케이션의 경우 자바스크립트 라이브러리를 통해 만들어진 위젯(tab, menu, calander 등)의 경우 이 위젯에 대한 의미 전달이 불분명할 경우 이에 대한 부가 설명을 추가할 수 있다.  

    `aria-describedby` 를 통해서 위젯과, 특정 섹션, element 그룹에 대한 부가적인 설명을 해줄 수 있다.

    예시: input validation 에러 메세지  

    ```html
    <label> 
    	<input
            *aria-describedby="error-message"*
    				<!-- ... 생략 ... -->
      />
    </label>
    </div>
    {validationError && (
      <p
        *id="error-message"* 
        tabIndex="-1"
    		<!-- ... 생략 ... -->
        >
        {validationError.errorMessage}
      </p>
    </div>

    ```

    ![%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/_2021-04-15__4.18.35.png](%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/_2021-04-15__4.18.35.png)

- **aria-required**

    폼이 제출되기 위해서는 필수적으로 입력을 해야하는 인풋 요소에 사용. 

    html attribute `required` 속성을 사용하는 것이 권장. 

    ```html
    <label for='email'> // react에서는 htmlFor 
    	<input
    	    type="email"
    	    name="email"
    	    placeholder="가입한 이메일을 입력해주세요."
    			aria-describedby="error-message"
    			required  
    			<!-- aria-required="true"-->
    	  />
    <label>
    ```

- **aria-selected**

    탭(tab)과 함께 사용되는 사용되는 속성으로 특정 탭의 활성화 여부에 대한 boolean 값을 가진다. 

    eg. 리뷰 탭이 활성화되어 있는 경우에  true, 비활성화시 false.

    ```jsx
    <div aria-role="tablist"> 
    	<li
        role="tab"
        aria-selected={tabbedCategory === 'review'}
        aria-controls="review-panel"
        > { ... }</li>
    	<li
        role="tab"
        aria-selected={tabbedCategory === 'my-review'}
        aria-controls="review-panel"
        > { ... }</li>
    </div>
    <div role="tabpanel">
    	tab1
    </div>
    <div role="tabpanel">
    	tab2
    </div>
    ```

- **aria-hidden**

    `aria-hidden=true` 는 해당 element와, 그 하위(child) element를 접근성 트리에서 제거하는 역할을 한다. document flow 상에서 주요 콘텐츠와 관련이 없는 요소들을 접근성 트리에서 제거함으로써, 장애를 가진 사용자들의 사용 경험을 올려줄 수 있다. 

    - 도큐먼트에서 장식(decorative) 목적으로 사용되는 icon, image를 제거
    - 중복되는 텍스트
    - 숨겨진, 닫힌(collapsed) 컨텐츠

    > child element에 상속이 되기 때문에, focus가 되는 element, 혹은 그 parent element에 적용되어서는 안된다. parent element에서 `true` 값을 가지면, child에서 `false` 를 명시해도, element는 여전히 노출되지 않는다.
  
    ```jsx
    // bad 
    <div>
    	<button aria-hidden=true>로그인</button>
    <div>

    // correct
    <div>
    	<MeaninglessIcon aria-hidden=true />
    <div>
    ```

    > role="presentation", role="none" 은  콘텐츠를 가린다는 점에서 aria-hidden=true 와 비슷하다. 하지만, 이 둘은 semantic meaning만 제거되고, element 자체는 접근성 트리에서 남는다는 것이 다르다.

- **aria-live="token"**

---

## 3. Semantic HTML element

 

 Semantic HTML element를 사용하면, HTML 코드에 사용의도를 명확히 하여 개발자간의 소통이나 유지보수에 도움을 주기도 하고, SEO에도 도움이 된다.  하지만 무엇보다 스크린 리더와 같은 보조기구에서 document에 대한 여러가지 기능과 추가적인 정보를 제공해줄 수 있다. 

 예를들면,  <nav> 태그를 사용하는 경우 탐색 영역과 컨텐츠 영역을 구분지어 주기도 하고, <p> 태그를 사용하면 문단 별로 넘기기 기능을 해주기도 한다. 

### 3.1 Content Sectioning

- <header>

    `<header>` 요소는 페이지의 컨텐츠 영역에 들어서기 전에, 소개해주는 영역이라고 볼 수 있다. 브랜드 네임, 로고, 검색 영역, 사이트의 네비게이션 등을 일반적으로 포함한다. 

    ```html
    <header>
    	<h1 className='bline'>짐싸</h1>
    	<div>
    		<a href='www.zimssa.com'>
    			<span>
    				<i className="zimssa-logo" />
    			</span>
    		</a>
    		<button>앱 다운로드<button>
    	<div>
    <header>
    ```

    ![%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/_2021-04-15__5.24.36.png](%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/_2021-04-15__5.24.36.png)

- <footer>

    섹션 컨텐츠나 페이지 전체의 하단 영역에 위치하여, copyright, 이용약관, 사이트맵과 같은 데이터를 포함한다. 

    ```html
    <footer>
    	<ZimssaInfo />
    	<ZimssaSiteMap />
    	<ZimssaSupport />
    	<ZimssaSNS />
    </footer>
    ```

    ![%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/_2021-04-15__5.27.02.png](%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/_2021-04-15__5.27.02.png)

- <main>

     document의 가장 중요한 콘텐츠 영역. 해당 document의 중심적인 토픽에 대한 콘텐츠를 담고 있어야한다. `main` element는 하나의 페이지 내에서 유일해야한다. 

     각 페이지 별로 중복되는 영역중 핵심 토픽이 아닌 영역, 예를 들어 사이드바, 네비게이션 바와 같은 요소는 `<main>` 태그에 속해서는 안된다. 

    ```jsx
    <header>
     // 헤더
    </header>
    <aside>
    // 사이드 바
    </aside>
    **<main>**
    	<article>
    		<h2>게시글 목록</h2>
    		<ul>
    			<li>
    				<article><h3>게시글 제목</h3></article>
    			</li>
    			<li>
    				<article><h3>게시글 제목</h3></article>
    			</li>
    		</ul>
    	</article>
    **</main>** 
    <footer>
    // 푸터
    </footer>
    ```

- [<article>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/article)

     단독으로 배포가능한, 재사용이 가능한 단위일 때 사용한다. 블로그의 포스트, 뉴스나 매거진의 기사, 댓글 공간과 같은 곳이 `article` 태그의 대표적인 예.

     section과 마찬가지로, 특정 article 태그에는 `heading`을 달아주어서 해당 article을 구분할 수 있도록 해주는 것이 좋다.

    ```html
    <article>
    	<h2>기사 제목</h2>
    	<section> 
    		<h3>기사 본문</h3>
    		<p>블라블라..</p>
    	</section>
    	<section>
    		<h3>댓글 영역</h3>	
    		<article>
    			<h4>댓글 제목</h4>
    			<p>댓글 내용</p>
    			<time>Jan 1</time>
    		</article>
    	</section>
    </article>
    ```

- [<section>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/section)

    도큐먼트에서 일반적으로 독립적인 파트를 나타낼때 사용한다.

    이를 나타낼 수 있는 더 자세한 element가 없는 경우에 한하여 `<section>`을 사용해야한다.

    아래와 같이 다른 대안이 있는 element가 있는 경우, 해당 element를 사용한다. 

    - 컨텐츠가 주요한 컨텐츠 영역을 나타내면 `<main>` 태그를 사용한다
    - element를 스타일링하는 래퍼로 사용할때는 `<div>`를 사용한다.
    - 컨텐츠가 `<main>`이 아닌 부가적인 역할을 하는 경우에는 `<aside>`를 사용한다.

    ```html
    <section>
    	<h2> 머릿말 </h2>
    	<p> 문단 </p>
    </section>
    ```

- <nav>

    Navigation : 내비게이션 메뉴들은 탭과 달리 의미상 확연히 다른 페이지로 이동할 것이라 예측. 메뉴 간 연속성이 있으면 오히려 혼란의 가능성 야기. 아이콘 형태의 경우 관습성을 이용하는 것을 권장.

    > Tab : 서로 관련 있는 것들끼리의 논리적 묶음. 유저는 관습상 탭 내 다른 메뉴를 클릭하면 페이지는 전환되지만 의미상 유사한 페이지로 이동할 것이라 예측.

     <nav> 링크를 사용하면 `탐색 영역`과 `컨텐츠 영역`을 구분지을 수 있는데, 이는 스크린 리더 사용자에게 도움을 줄 수 있다. 

     문서의 모든 링크가 <nav> 요소 안에 있을 필요는 없다.  <nav>는 주요 탐색 링크에 대한 그룹을 묶어 주기 위한 요소이다.  <nav> 하나는 사이트 전체 탐색, 다른 하나는 현재 페이지 내 탐색으로 사용하는 등, 하나의 문서에서 여러 개의 [<nav>](https://developer.mozilla.org/ko/docs/Web/HTML/Element/nav) 태그를 가질 수 있다. (예를 들어, 헤더의 <nav>, crumb의 <nav>) 

    Breadcrumbs UI.  아래에 링크 그룹을 <nav> 요소를 사용하여 묶을 수 있다. 

    ```html
    <nav>
    	<ul>
    		<li>짐싸 팀</li>
    		<li>Docs</li>
    		<li>짐싸 WAI-ARIA 가이드라인</li>
    	</ul>
    <nav>
    ```

    ![%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/_2021-04-15__5.01.45.png](%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/_2021-04-15__5.01.45.png)

- [<aside>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/aside)

     메인 컨텐츠와 직접적으로 연관이 있지 않는 경우에 `<aside>` 태그를 사용. 사이드바가 대표적인 예.  

    ```html
    <aside>
    	<div>
    		<h3>워크스페이스</h3>
    	</div>
    	<div>
    		<ul>
    			<li>OKR</li>
    			<li>짐싸</li>
    			<li>짐싸 팀</li>
    		</ul>
    	<div>
    <aside>
    ```

    ![%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/_2021-04-15__5.00.47.png](%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/_2021-04-15__5.00.47.png)

- [<figcaption>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/figcaption)
- [<figure>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/figure)
- [<time>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/time)

### 3.2 Text content

- div
  
    **The HTML Content Division element (<div>) is the generic container for flow content.**

     div 태그는 문서의 flow를 구분하기 위한 것으로, 그 자체로는 아무런 의미가 없다.
    div가 사용되는  케이스에 대해 정리하면 아래와 같다.

    - article, nav, button 등의 다른 적절한 semantic element 도저히 없을때.
    - 특정 부분을 wrapping하여 style을 넣어주기 위해 구분할때.

- p

    문단의 기능을 하는 태그. 

    콘텐츠를 문단을 통해 구분하면,  보조 기기에서 문단 넘기기 기능을 사용할 수 있기 때문에1234

     접근성을 높여준다.

- ul / ol
- dl, dt, dd

  `<ul>`태그와 `<li>`태그는 리스트에 대한 나열인 반면,  dl, dt, dd는 **name-value**의 관계를 가지는 리스트들에 대한 그룹을 지을때 사용한다.
  
  용어 사전(dictionary)에 사용될 수도 있고, 메타 데이터를 정렬하여 표현하고 싶은 경우에도 사용이 가능하다. 

    ```jsx
    <article>
    	<div>
    		// 사진 영역
    	</div>
    	<div>
    		// ...
    		<dl>
    			<dt>이사</dt>
    			<dd>4건</dd>
    			<dt>리뷰</dt>
    			<dd>0건</dd>
    			<dt class="blind">별점</dt>
    			<dd>0.0</dd>
    		</dl>
    	<div>
    <article>
    ```

    ![%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/_2021-04-16__9.47.38.png](%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/_2021-04-16__9.47.38.png)

    ```jsx
    //그외 사용법
    //case1
    <dl>
    	<dt>저자</dt>
    	<dd>A</dd>
    	<dt>공저</dt>
    	<dd>B</dd>
    	<dt>번역</dt>
    	<dd>C</dd>
    </dl>
    // case2
    <dl>
     <dt> 최근 수정일 </dt>
     <dd> 2004-12-23T23:33Z </dd>
     <dt> 업데이트 주기</dt>
     <dd> 60s </dd>
     <dt> 저자 </dt>
     <dt> 에디터 </dt>
     <dd> Robert Rothman </dd>
     <dd> Daniel Jackson </dd>
    </dl>
    ```

- figure

---

## 4. Rules

1. 사용 의미에 해당하는 HTML 요소가 존재 할 경우...
2. ㅁㄴㅇㄹ

---

## 5. Use cases

### 로그인 form

![%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/_2021-04-15__3.16.51.png](%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/_2021-04-15__3.16.51.png)

```jsx
<form onSubmit={handleLogin}>         
    <label className="blind" htmlFor='email'>
        이메일 :
    </label>
    <input
        type="email"
				id="email"
        placeholder="가입한 이메일을 입력해주세요."
				required
        aria-describedby="error-message"
      />
    <label className="blind" htmlFor="password">
        비밀번호 : 
    </label>
    <input
        type="password"
				id="password"
        placeholder="비밀번호를 입력해주세요."
				required
        aria-describedby="error-message"
      />
    </div>
    {error && (
      <p
        id="error-message"
        tabIndex="-1"
      >
        {error.message}
      </p>
    )}
  </div>
  <button
		aria-describedby="descriptionLoginBtn"
    type="submit"
    disabled={!isBtnLoginActive}
  >
    로그인
  </button>
	<p id="descriptionLoginBtn" className="blind">버튼 클릭시 로그인이 됩니다.</p>
</form>
```

### 페이지 내비게이션

![%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/Screen_Shot_2021-04-15_at_3.23.09_PM.png](%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/Screen_Shot_2021-04-15_at_3.23.09_PM.png)

```jsx
<div className={cx('tabbar', 'bg-gray-opacity-50', { visible: visible })}>
	<div key={index} className={cx('item', 'on')}>
    <img src={item.imageOn} alt={item.text} />
    <p className={cx('text-caption-bold', 'color-primary-500')}>
      {item.text}
    </p>
  </div>
	<div key={index} className={cx('item', 'off')}>
	  <Link to={item.link}>
	    <img src={item.imageOff} alt={item.text} />
	    <p className={cx('text-caption')}>{item.text}</p>
	  </Link>
	</div>
	<div key={index} className={cx('item', 'off')}>
	  <Link to={item.link}>
	    <img src={item.imageOff} alt={item.text} />
	    <p className={cx('text-caption')}>{item.text}</p>
	  </Link>
	</div>
</div>
```

### 탭(tab)

![%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/_2021-04-15__3.24.59.png](%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/_2021-04-15__3.24.59.png)

```jsx
// 탭 영역
<div
  role="tablist"
  className={cx('tab-menu', 'bg-surface-base', 'text-bodytext2')}
>
    <button
      role="tab"
      aria-selected={tabbedCategory === 'my-review'}
      aria-controls="my-review-panel"
     >
      내 리뷰
    </button>
    <button
      role="tab"
      aria-selected={tabbedCategory === 'reviews'}
      aria-controls="review-panel"
     >
			기사님 리뷰
		</button>
</div>

// 탭 패널 
<article id="review-panel" role="tabpanel">
	<h2 className='blien'>기사님 이사 후기 리스트</h2>
  <ul>
    {partnerReviewListData.size > 0 ? (
      <ServiceReview partnerReviewListData={partnerReviewListData} />
    ) : (
      <EmptyBox />
    )}
  </ul>
</article>
```

### 프로필

![%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/_2021-04-16__9.47.38.png](%E1%84%8C%E1%85%B5%E1%86%B7%E1%84%8A%E1%85%A1%20WAI-ARIA%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%201bdb28ae2f24407cbc479fc51d6a2aac/_2021-04-16__9.47.38.png)

```html

```
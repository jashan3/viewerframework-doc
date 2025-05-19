# How to start


### 1. 라이브러리 다운로드
- viewerjs.[contenthash].js


### 2. pdf 프레임워크 시작 파라미터 세팅

- window에 ViewerJS 전역변수로 선언된 상태.

```javascript
const pdfCore = new ViewerJS.PdfCore();
const initPdfParms = {
    url: "<pdf url>",
    cMapUrl: "<cmap 폴더 url>/",
    standardFontDataUrl: "<fontSet 폴더 url>/",
    wasmUrl: "<wasmUrl 폴더 url>",
    options: {
        '<기존 암호화에 필요한 데이터>'
    }
}
await pdfCore.init(initPdfParms);
```

### 3. 폴더구조 세팅
```
루트/
├── 📂 cmaps
├── 📂 standard_fonts
└── 📂 wasm
└── viewerjs.js
```

<br>
<br>
<br>
<br>

# 함수 (Function)

이 문서는 PDF 프레임워크 관련 주요 함수 설명을 정리합니다.

## `init`  
**설명**

pdf core 초기화 함수  

**Parameters**  
| `type` | name | description |
|--------|------|-------------|
| `InitPdfParams` | params | pdf초기화 함수 |

**Returns**  
- 없음 (None)

**example**  
```javascript
// PdfCore 객체 선언
this.pdfCore = new PdfCore();

const viewerId = 'viewer';
const samplurl1 = sampleJSON[index].url;
await this.pdfCore.init({ url: samplurl1, viewerId: viewerId });
```

---

## `findToc`  
**설명**

목차 찾기 기능, 
onOutlineReady호출 이후 정확한 목차 찾기 기능이 작동될수있다.


**Parameters**  
| `type` | name | description |
|--------|------|-------------|
| `number` | findPageNum | 페이지 번호 |

**Returns**  
- 없음 (None)

---

## `setPageMode`  
**설명**

 페이지 모드 변경  

`single`: 단면

`dual`: 양면

`firstdual`: 첫페이지 빈 양면

`scroll`: 스크롤

**Parameters**  
| `type` | name | description |
|--------|------|-------------|
| `string` | mode |  |

**Returns**  
- 없음 (None)

---

## `gotoNextPage`  
**설명**

다음 페이지로 이동  

**Parameters**  
- 없음 (None)

**Returns**  
- 없음 (None)

---

## `gotoPrevPage`  
**설명**

 이전 페이지로 이동  

**Parameters**  
- 없음 (None)

**Returns**  
- 없음 (None)

---

## `gotoPage`  
**설명**: 페이지 이동  

**Parameters**  
| `type` | name | description |
|--------|------|-------------|
| `number` | page | 페이지 번호 |

**Returns**  
- 없음 (None)

---

## `gotoSearchPage`  
**설명**

검색 페이지 이동  

**Parameters**  
| `type` | name | description |
|--------|------|-------------|
| `SearchMatch` | searchParam | 검색어 파라미터 |

**Returns**  
- 없음 (None)

---

## `setScaleIncrease`  
**설명**

 스케일 증가 0.1씩  

**Parameters**  
- 없음 (None)

**Returns**  
- 없음 (None)

---

## `search`  
**설명**

 전체 페이지를 순회하며, 검색어를 포함하는 결과를 콜백으로 전달합니다.  

**Parameters**  
| `type` | name | description |
|--------|------|-------------|
| `string` | keyword | 검색어 |
| `SearchCallback` | callback | 검색 콜백 함수 |

**Returns**  
| `type` | name | description |
|--------|------|-------------|
| `Promise<boolean|null>` |  | 검색 종료 |

---

## `stopSearch`  
**설명**

진행 중인 검색을 중단하는 함수  
이 함수를 호출하면 현재 진행 중인 검색 중지됩니다.

---

## `annotationEditMode`  
**설명**

수정모드 on/off  

**Parameters**  
| `type`   | name    | description       |
|----------|---------|-------------------|
| boolean  | isStart | 수정모드 (true:on, false:off) |

---

## `changeAnnotationType`  
**설명**

필기모드 변경, 변경 시 수정모드도 true  

**Parameters**  
| `type`  | name | description         |
|---------|------|---------------------|
| string  | type | 필기모드 타입 (Ink: 자유선, Line: 직선, Normal: 선지우개, Object: 객체지우개) |

---

## `changeAnnotationColor`  
**설명**

색상 변경  

**Parameters**  
| `type`        | name  | description               |
|---------------|-------|---------------------------|
| number[]      | color | 색상 rgb 값 array 길이 3 (ex: [255,255,255]) |

---

## `changeAnnotationOpacity`  
**설명**

불투명도 변경  

**Parameters**  
| `type`  | name    | description  |
|---------|---------|--------------|
| number  | opacity | 불투명도     |

---

## `changeAnnotationBorderWidth`  
**설명**

필기 두께 변경  

**Parameters**  
| `type`  | name  | description  |
|---------|-------|--------------|
| number  | width | 필기 두께    |

---

## `changeAnnotationEraserBorderWidth`  
**설명**

지우개의 두께 변경  

**Parameters**  
| `type`  | name  | description  |
|---------|-------|--------------|
| number  | width | 지우개 두께  |

---

## `removeAnnotation`  
**설명**

annotation 제거  

**Parameters**  
| `type`             | name          | description      |
|--------------------|---------------|------------------|
| string \| number    | annotationId  | 삭제할 대상 id   |

---

## `modifyAnnotation`  
**설명**

annotation 수정  

**Parameters**  
| `type`         | name                | description       |
|----------------|---------------------|-------------------|
| AnnotationData | willEditedAnnotation | 수정할 annotation |

---

## `importAnnotations`  
**설명**

annotation 저장  

**Parameters**  
| `type`              | name        | description               |
|---------------------|-------------|---------------------------|
| AnnotationData[]    | annotations | 배열로 된 annotation 객체 |

---

## `exportAnnotations`  
**설명**

 annotation 추출  

**Parameters**  
- 없음 (None)

**Returns**  
| `type` | name | description |
|--------|------|-------------|
| `Object[]` |  | 추출한 annotation array값 |

---

## `pdfToImage`  
**설명**

 PDF 페이지를 이미지로 추출 요청  

**Parameters**  
| `type` | name | description |
|--------|------|-------------|
| `number` | page |  |
| `number` | targetWidth |  |
| `number` | targetHeight |  |

**Returns**  
| `type` | name | description |
|--------|------|-------------|
| `string` |  | 현재 PDF 페이지에 대한 base64 이미지 |

---

## `print`  
**설명**

프린트 기능 작동  

**Parameters**  
- 없음 (None)

**Returns**  
- 없음 (None)

---

<br>
<br>
<br>
<br>

# 객체 타입 (Object Types)

이 문서는 PDF 뷰어 관련 주요 객체 타입들의 속성(property) 및 설명을 정리합니다.

## `AnnotationData`

> 주석(annotation)에 대한 정보를 담는 객체 타입입니다.

| 타입 (Type) | 이름 (Name) | 설명 (Description) |
| --- | --- | --- |
| `string \| number` | `id` | 주석의 고유 식별자 |
| `string` | `subtype` | 주석의 유형 ("Ink"=자유선, "Line"=직선) |
| `number[]` | `color` | 색상 (RGB 배열 [255, 0, 0] 형식) |
| `number` | `opacity` | 색 투명도 (0.0 ~ 1.0) |
| `number` | `pageNum` | 주석이 위치한 페이지 번호 |
| `number` | `width` | 선 너비 |
| `Date` | `modificationDate` | 수정일자 |
| `Date` | `creationDate` | 생성일자 |
| `number[] \| undefined` | `lineCoordinates` | 직선 좌표 (예: [x1, y1, x2, y2]) (선택적 속성) |
| `number[][] \| undefined` | `inkLists` | 자유선 좌표 목록 (예: [[x1, y1], [x2, y2], ...]) (선택적 속성) |

---

## `SearchMatch`

> 검색 결과 항목을 나타내는 객체 타입입니다.

| 타입 (Type)           | 이름 (Name) | 설명 (Description)          |
| --------------------- | ----------- | --------------------------- |
| `number`              | `index`     | 검색 결과 내의 인덱스       |
| `string`              | `match`     | 매칭된 키워드 또는 문구     |
| `number`              | `pageNum`   | 매칭된 페이지 번호          |
| `string`              | `snippet`   | 주변 문맥 텍스트            |
| `string \| undefined` | `tocTitle`  | (선택) 목차에서의 섹션 제목 |

---

## `InitPdfParams`

> PDF 뷰어 초기화 시 전달하는 설정 객체 타입입니다.

| 타입 (Type) | 이름 (Name) | 설명 (Description) |
| --- | --- | --- |
| `string \| undefined` | `viewerId` | PDF 뷰어를 렌더링할 DOM 요소의 ID |
| `'single' \| 'dual' \| 'firstdual' \| 'scroll' \| string \| undefined` | `pageMode` | 페이지 표시 모드 (선택적 속성) |
| `number \| undefined` | `pageNum` | 초기 로딩할 페이지 번호(선택적 속성) |
| `string \| undefined` | `cMapUrl` | 문자 맵(CMap) 리소스 경로 (PDF.js 용) |
| `string \| undefined` | `standardFontDataUrl` | 기본 폰트 데이터 리소스 경로 (PDF.js 용) |
| `string \| undefined` | `wasmUrl` | WebAssembly 모듈 경로 (PDF.js 용) |

---

## `TocItem`

> 목차 아이템을 표현하는 객체 타입입니다.

| 타입 (Type) | 이름 (Name) | 설명 (Description)                |
| ----------- | ----------- | --------------------------------- |
| `string`    | `title`     | 목차 제목                         |
| `number`    | `depth`     | 목차 깊이 (예: 1=챕터, 2=섹션 등) |
| `number`    | `pageNum`   | 해당 항목이 나타나는 페이지 번호  |


---
<br>
<br>
<br>
<br>
<br>

# 콜백 함수 (Callback Function)

이 문서는 PDF 뷰어 관련 주요 콜백 함수의 속성(property) 및 설명을 정리합니다.


**example**  
```javascript
    this.pdfCore = new PdfCore();
    /**
     * pdf core callback
     */
    this.pdfCore.callbackOpt = {
        onClick: ...,
        onPageChanged: ...,
        onLastPage: ...,
        onFirstPage: ...,
        onOutlineReady: ...,
        onScaleChanged: ...,
        onAnnotationHistoryChanged: ...,
    }
```


## `SearchCallback`  
**설명**

해당 페이지에서 발견된 검색 결과 리스트

**Parameters**  
| type | name | description |
|--------|------|-------------|
| `string` | matches | pdf초기화 함수 |
| `SearchMatch[]` | matches | 해당 페이지에서 발견된 검색 결과 리스트 |
| `number` | findKeywordCount | 검색어 찾은 갯수 |
| `boolean` | isLastPage | 마지막 검색페이지인지 여부 |

**example**  
~~~javascript
// PdfCore 객체 선언
this.pdfCore = new PdfCore();
const searchCallback = (keyword, result, total, end) => {
    if (result.length > 0) {
        for (let it of result) {
        setTimeout(() => {
            resultsTotalSpan.textContent = total;
            const div = document.createElement('div');
            div.textContent = it.snippet;
            div.style.paddingTop = '10px';
            div.style.paddingBottom = '10px';
            div.dataset.pagenum = it.pageNum;
            div.style.cursor = 'pointer';
            div.addEventListener('click', async e => {
                e.preventDefault();
                //검색페이지 이동 처리
                await this.pdfCore.gotoSearchPage(it);
            });
            resultsContainer.appendChild(div);
        }, 0);
        }
    }
    else {
        //empty
    }
}
//검색 시작
this.pdfCore.search(searchInput.value, searchCallback);
~~~


## `onClick`
  
**설명**

클릭 이벤트 콜백 - 사용자가 클릭한 위치의 좌표 콜백


**Parameters**  
| type | name | description |
|--------|------|-------------|
| `number` | x | document의 x축 좌표 |
| `number` | y | document의 y축 좌표 |

**example**  
~~~javascript
this.pdfCore.callbackOpt = {

    onClick: (x, y) => {
        console.log(x, y);
    },
}
~~~


## `onPageChanged`
  
**설명**

페이지 변경 이벤트 콜백


**Parameters**  
| type | name | description |
|--------|------|-------------|
| `number` | currentPage | 현재 페이지 |
| `number` | totalPages | 전체 페이지 수 |
| `string \| undefined` | tocTitle | 목차 제목 |

**example**  
~~~javascript
this.pdfCore.callbackOpt = {
    /**
     * 페이지 변경시 리스너
     * @param {number} page 현재 페이지
     * @param {number} total 전체 페이지
     * @param {string} tocTitle 목차 제목
     */
    onPageChanged: (page, total, tocTitle) => {

    },
}
~~~

## `onFirstPage`

  
**설명**

 첫 페이지에 도달후 한번더 첫 페이지로 이동을 시도 했을때 콜백


**Parameters**  
없음

**example**  
~~~javascript
  this.pdfCore.callbackOpt = {
    onFirstPage: () => {

    },
  }
~~~

## `onLastPage`

  
**설명**

 마지막 페이지에 도달후 한번더 마지막 페이지로 이동을 시도 했을때 콜백


**Parameters**  
없음

**example**  
~~~javascript
this.pdfCore.callbackOpt = {
    onLastPage: () => {

    },
}
~~~


## `onOutlineReady`

  
**설명**

목차 파싱이 완료됬을때 콜백


**Parameters**  
| type | name | description |
|--------|------|-------------|
| `TocItem` | toc | 목차 아이템 객체 |

**example**  
~~~javascript
this.pdfCore.callbackOpt = {
    /**
     * 목차 파싱 완료 
     */
    onOutlineReady: (toc) => {

    },
}
~~~


## `onScaleChanged`

  
**설명**

스케일이 변경될때 콜백


**Parameters**  
| type | name | description |
|--------|------|-------------|
| `number` | scale | 뷰잉중인 pdf scale 값 |

**example**  
~~~javascript
this.pdfCore.callbackOpt = {
    /**
     * 스케일 변경 콜백
     */
    onScaleChanged: (scale) => {

    },
}
~~~


## `onAnnotationHistoryChanged`

  
**설명**

필기모드 history 변경 콜백


**Parameters**  
| type | name | description |
|--------|------|-------------|
| `boolean` | prev | 이전 필기 history가 존재할때 |
| `boolean` | next | 다음 필기 history가 존재할때 |

**example**  
~~~javascript
this.pdfCore.callbackOpt = {
    /**
     * 필기 히스토리 변경 콜백
     */
    onAnnotationHistoryChanged: (prev,next) => {

    },
}
~~~
# DOM_study

DOM을 깨우치다 (코디 린들리 저) 에서 기억해 두면 좋을 만 한 내용들을 기록해 두는 곳 

- 🎉 2021.09.17 DOM 정리 시작 

> 노드

노드 개체 유형 

1) DOCUMENT_NODE : window.document 등
2) ELEMENT_NODE : body, a, p ,script, style,html ,h1 등 
3) ATTRIBUTE_NODE : class="funEdges" 등 
4) TEXT_NODE: 줄바꿈과 공백을 포함한 HTML 문서 내의 텍스트 문자
5) DOCUMENT_FRAGEMENT_NODE : document.createDocumentFragement()
6) DOCUMENT_TYPE_NODE : <!DOCTYPE html> 

모든 노드는 Node로 부터 상속받은 nodeType 및 nodeName 속성을 가진다 

- createAttribute() 메서드는 사용이 금지되었으며, attribute 노드를 만드는데 사용해서는 안된다 대신에, setAttribute(), getAttribute(), removeAttribute()를 사용해야한다 

- innerHTML의 경우에는 HTML 파서를 호출해서 비용이 많이 소요되어 가급적 사용을 피하고 textContent등을 사용한다 

- removeChild() 및 replaceChild()를 사용하여 노드를 제거하거나 바꿀 수 있다 

: DOM에서 노드를 제거하는 것은 여러 단계를 거치는데 먼저 삭제하고자 하는 노드를 선택하고 다음으로는 부모노드에 대한 접근을 얻는다 이때 보통 parentNode속성으르 사용한다 부모노드에서 삭제할 노드에 대한 참조를 전달하여 removeChild() 메서드를 호출한다 -> divA.parentNode.removeChild(divA)

- 노드 컬렉션에 대한 이해 

: 트리에서 노드 그룹을 선택하거나 사전에 정의된 노드 집합에 접근하려면, 해당 노드들이 NodeList나 HTMLCollection내에 있어야한다 

해당 노드 컬렉션들의 특징 
1) 컬렉션은 라이브 상태 혹은 정적 일 수 있다 이는 컬렉션 내에 포함된 노드들이 현재문서 또는 현재 문서에 대한 스냅샷의 일부라는 것이다 
2) 노드는 트리 순서에 따라서 정렬이 된다 이 순서는 트리 루트로부터 분기점까지의 선형경로와 일치한다
3) 컬렉션은 리스트 내의 요소 개수를 나타내는 length속성을 가진다

-> 직계 자식 노드 전부에 대한 리스트 얻기  : document.querySelector('부모노드이름').childNodes 

- text와 comment 노드를 무시하고 DOM을 탐색할때 사용하는 것 
: firstElementChild, lastElementChild, nextElementSibling, previousElementSibling, children, parentElement 

> DOCUMENT

- document 노드는 DocumentType 노드 개체 하나(ex: <!DOCTYPE html>) , Element 노드 개체하나( ex: <html lang="en">)을 가질 수 있다 
  
> ELEMENT
  
- element 생성 : document.createElement('textarea')
  
- element 태그 이름 얻기: document.querySelector('a').tagName = > A 
  
- element attribute 및 값에 대한 리스트 컬렉션 얻기 : var attr =  document.querySelector('a').attributes; 
  
  출력시 : for (let i = 0; i< attr.length; i++){ console.log(attr[i].nodeName + '=' + attr[i].nodeValue); }
                                       
  (*유의점: attribute속성을 반환하는 배열은 라이브 상태라는 것을 고려해야한다, 내용물은 언제든지 바뀔 수 있다 해당 속성보다는 getAttribute, setAttribute, hasAttribute, removeAttribute등을 사용하는 것이 좋다)

- element의 attribute 값 획득 설정 제거 하기 , 특정 attribute를 가지고 있는지 확인하기
                                       
예시) div1.removeAttribute('class') / div1.setAttribute('class','div1') / div1.getAttribute('class') / div1.hasAttribute('class') 
                                       
- class attribute 값 리스트 얻기 : div1.classList => {0='class1',  1 ='class2'} 식으로 값이 얻어진다 div1.className의 경우 해당 element가 class를 여러개 가지고 있을 경우  띄어쓰기를 한 상태로 값을 얻어낼 수 있다 
  
- class attribute에 하위 값 추가 및 제거하거나  toggle하기 : div1.classList.add('new') / div1.classList.remove('old') / div1.classList.toggle('new') (*toggle의 경우 new class가 있을 경우 해당 값을 class에서 제거해주고 없을 경우 class에 추가해 준다) 
  
- class attribute 가 특정 값을 가지고 있는지 확인 : div1.classList.contains('new') => 해당 값을 가지고 있다면 true 반환 없다면 false를 반환한다 
  
- data-* attribute를 가져오고 설정하기
  
: element 노드의 dataset속성은 element에서 data-*로 시작하는 모든 attribute를 가진 개체를 제공해준다 

  ex) <div data-old-new="state" data-n1-n2="node"></div>
  
  ele.dataset.oldNew => state출력  ele.dataset.n1N2 => node가 출력됨  / dataset은 data attribute들의 camelCase 버전을 가지고 있다 그래서 -으로 연결된 문자들은 첫글자를 대문자로 대체하여 표현하는 camelCasing을 대체된다 
 
  
> Element 노드 선택 
  
- 특정 element 노드 선택하기 : querySelector(), getElementById() 
  
- element 노드 리스트 선택 및 생성하기: querySelectorAll(), getElemetsByTagName(), getElementsByClassName() 
  
🎨 2021.09.18 요소의 위치들 알아내기
  
> Element 노드 지오메트리와 스크롤링 지오메트리 
  
- offsetParent를 기준으로 element의 offsetTop 및 offsetLeft의 값 가져오기
  
: offsetTop, offsetLeft를 활용하면 offsetParent로 부터 element 노드의 오프셋 픽셀 값을 가져올 수 있다. 이때 가장 가까운 부모 element 중에서 position이 absolute가 아닌 경우 body나 document에 해당하는 것이 기준이 된다 
  
부모 요소(자신을 감싸고 있는 요소)의 position이 absolute인 경우에는 해당 부모 요소를 기준으로 위치를 계산한다 
  
- getBoundingClientRect() 를 사용하여 뷰포트를 기준으로 element의 top,right,bottom,left 테두리의 오프셋을 얻기
  
  : viewport(브라우저)의 좌상단 끝을 기준으로 element가 브라우저에서 그려질때 element의 바깥쪽 테두리의 위치를 얻을 수 있다. 
  
  var divEdges = document.querySelector(element이름).getBoundingClientRect() 를 하게 되면 각각 divEdges.top, divEdges.right, divEdges.bottom, divEdges.left 순서대로 값을 얻어 낼 수 있다  
  
=> 해당 기능은 유저가 마우스 커서를 어디에 위치시키냐에 따라서 상태를 변하게 하는데 편하다 예시) 마우스 위를 움직이면서 별점 container안의 별들이 색칠되는 등의 효과표현
  
- 뷰포트에서 element의 크기(테두리+ 패딩+ 내용) 얻기
  
: getBoundingClientRect()를 사용하게 되면 top, right, bottom, left와 더불어 height와 width 값을 가지고 있는 개체를 얻을 수있다. 이때, element의 크기는 div의 내용, 패딩, 테두리를 모두 더한 것이다 
  
- 뷰포트에서 border(테두리)를 제외한 element크기(패딩+내용)얻기 : div.clientHeight, div.clientWidth / 각각 패딩 내용만을 고려한 너비와 높이값을 알아낼 수 있다 
  
- scrollHeight와 scrollWidth를 사용하여 스크롤될 element의 크기 얻기 
  
: 웹 브라우저에서 스크롤되는 html 문서를 열고 <html>나 <body>의 속성에 접근하면, 스크롤될 html문서의 전체 크기를 구할 수 있다. / 만약 특정 노드 안의 길이를 구하고 싶을때에도 사용이 가능하다 
  
  ex) div의 너비와 높이는 모두 100이고 p가 1000일때 <div><p></p></div> 에서 div.scrollHeight와 div.scrollWidth를 구하게 되면 모두 1000이 출력이 된다 
  
 => 유저가 스크롤 하면서 길이에 따른 다른 animation적용하기에 활용 가능하다 
  
  (*만약, 스크롤될 노드가 스크롤 영역보다 작은 경우, 스코롤 가능한 영역 내의 포함된 노드의 크기를 판별하려면 clientHeight,clientWidth를 사용한다)
  
- 스크롤 된 top과 left값을 구하고 싶다면 스크롤영역가리키는element.scrollTop(또는 .scrollLeft)를 사용하여 값을 구할 수 있다.
  
⏰ 2021.09.19  element 노드 인라인, textNode
  
> element 노드 인라인 스타일 
  
주의점: css에서 변수에 사용하는 -의 경우 js에서 style개체로 접근할때에는 이를 제거 하고 카멜케이스를 사용한다 (ex: font-size -> fontSize) 또한 css 속성명이 javascript의 키워드일 경우 css라고 접두어가 붙는다 (ex: float -> cssfloat) 

- css속성 조작하는데 사용하는 메서드: 
  
 setProperty(propertyNamem value) / setPropertyValue(propertyName) / getPropertyValue(propertyName) / removeProperty(propertyName) 
  
 (*유의점: setProperty와 getPropertyValue 메서드에 전달되는 속성명은 하이픈이 포함된 css 속성명을 사용한다 

 > Text 노드 
  
 :html 문서가 해석 될때, html 페이지의 element 사이에 섞여 있는 테스트는 text 노드로 변환된다  / 공백노드와 줄바꿈 또한 text 노드로 만들어진다 
  
 - text 노드 생성 및 삽입하기 : createTextNode('text내용들') 으로 생성 한 후 다른 노드들과 같이 appendchild를 활용해 삽입한다 
  
 - data나 nodeValue로 text 노드 값 가져오기 : text값을 얻고자 하는 노드.firstChild.data(또는 .nodeValue)로 한다 
  
 - textContent와 innerText간의 차이: 
  
1) innerText에는 css가 반영이 된다 (숨겨진 텍스트가 있을 경우 innerText는 해당 텍스트를 무시하는 반면, textContent는 무시하지 않는다) 
2) innerText는 css 영향을 받기 때문에 리플로우(* 문서 내 노드들의 레이아웃, 포지션을 제거한 후 다시 뿌려주는 것 퍼포먼스 저하를 유발시키는 프로세스) 가 발생하는 반면, textContent는 그렇지 않다
3) innerText는 <script>와 <style> element내에 포함된 text 노드를 무시한다 
4) innerText는 텍스트를 정규화해서 반환한다 (*마크업만 제거하여 그대로 반환하는 것)
5) innerText는 비표준으로 브라우저에 국한되지만, textContent는 DOM사양으로 구현되고 있다 
  
  
🎃 2021.09.21 documentfragment 노드, css 규칙
   
> DocumentFragment 노드 
  
: DocumentFragment노드를 생성해서 사용하게 되면 라이브 DOM 트리 외부에 경량화 된 문서 DOM을 만들 수 있다 즉, DocumentFragment는 메모리상에서만 존재하는 빈 문서 템플릿이다 
  
 - DocumentFragment 생성하기 : let 변수노드 = document.createDocumentFragment() 로 생성 
  
 Fragment 사용하여 새롭게 생성한 노드 요소들을 구조에 삽입하는 것에는 다음과 같은 장점들이 있다 
  
 1) DocumentFragment는 어떤 종류의 노드(<body> <html>은 제외)도 가질 수 있는 반면 , element는 그렇지 ㅇ낳다 
 2) DocumentFragment는 DOM에 추가하더라도 DocumentFragment 자체는 추가되지 않으며, 노드의 내용만이 추가된다 
 3) DocumentFragment를 DOM에 추가할 때, DocumentFragment는 추가되는 위치로 이전되며, 생성한 메모리상의 위치에 더 이상 존재하지 않는다 / 노드를 포함하기 위해 일시적으로 사용된 후 라이브 DOM으로 이동되는 element노드는 그렇지 않다 
  
 예시 : 
  let ul = document.querySelector(ul)
  
  let docFrag = document.createDocumentFragment();
  
  ["blue","green","red"].forEach(function(e){
    let li = document.createElement('li'); 
    li.textContent = e;
    docFrag.appendChild(li);
  });
 
  ul.appendChild(docFrag);
  
  body안에는 "<ul><li>blue</li><li>green</li><li>red</li></ul>" 이 최종적으로 들어가게 된다 
  

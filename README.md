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

                                     

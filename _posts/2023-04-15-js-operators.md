---
layout: post
title: "📭FormData+Ajax"
---

- `updateForm`에 담을 input은 `elem` 클래스 추가
- `updateForm.append`로 넘길 데이터 생성
- `contentType, processData`은 `false` 필수

```jsx
const dataUpdate = (e) => {
  const _row = e.closest('tr'); //row
  let dataUpdateArray = []; //row data array

  for (const inp of _row.querySelectorAll('.elem')) { //row input
    dataUpdateArray.push(inp.value);
  }

  let updateForm = new FormData();
  updateForm.append('status',dataUpdateArray[0]);
  updateForm.append('price1',dataUpdateArray[1]);
  updateForm.append('price2',dataUpdateArray[2]);
  updateForm.append('price3',dataUpdateArray[3]);
  

  let updateUrl = 'url';
  $.ajax({
    url : updateUrl,
    type : 'post',
    data : updateForm,
    cache : false,
    contentType : false,
    processData : false,
    dataType: "json",
    error : function(jqXHR, textStatus, errorThrown) {

    },
    success : function(result, jqXHR, textStatus){
      if(result['result']==true){
        alert(`${result['status']}\n${result['price1']}\n${result['price2']}\n${result['price3']}`);
      }
    }
  });
  
  console.log(dataUpdateArray);
}

```

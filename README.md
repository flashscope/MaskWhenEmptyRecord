# MaskWhenEmptyRecord
마스크가 언제 매진되었는지 기록합니다.
<br>
<br>마스크를 지도에서 보며 재고를 확인하는 것은 대기업을 비롯하여 많은 개발자분들이 만들어 주셨습니다.
<br>하지만 제공되는 api를 사용해도 현실적인 문제 (전산 입력 지연이나 오류)가 많다 보니 이를 보조할 지표 하나를 더 만들고자 합니다.
<br>약간 늦은 감이 있지만 17일부터(18일부터 확인 가능) 그날의 입고, 매진 시간을 기록하여 여기에 공개합니다.
<br>해당 약국의 현재 재고뿐만이 아니라 저번 주 같은 요일의 입고된 시간이나 매진된 시간을 참고하면 좀 더 편리한 구매가 가능하게 될 것으로 기대해봅니다.
<br>
<br>다만 서버 문제 등으로 실시간이나 멋진 UI로 보여드리지는 못하고 매일 밤 간단하게 가공해서 다른 개발자분들이 이용하실 수 있도록 제공합니다.

## 이용 방법
정부의 API를 수집해서 이용하고 있습니다.
<br>https://app.swaggerhub.com/apis-docs/Promptech/public-mask-info/20200307-oas3#/
<br>
<br>약국정보는 https://8oi9s0nnth.apigw.ntruss.com/corona19-masks/v1/stores/json 에서 제공 중이며
<br>가져오실 때 스키마의 code로 약국의 시간 정보를 찾으시면 됩니다.
<br>
<br>저는 프론트 개발자가 아니다 보니 어떤 식으로 제공해 드리는 게 좋을지 몰라서
<br>임의대로 hash = code % 1000으로 파일 천 개에 나누어서 커밋을 합니다.
<br>https://raw.githubusercontent.com/flashscope/MaskWhenEmptyRecord/master/datas/maskRecord-<hash\>.json
<br>
<br>만약 code가 11856777인 약국을 찾으시려면 code % 1000 = 777이므로
<br>https://raw.githubusercontent.com/flashscope/MaskWhenEmptyRecord/master/datas/maskRecord-777.json
<br>에서 해당 약국의 정보를 찾으시면 됩니다.
<br>
  
## 스키마
해당 json 파일에서 약국의 code를 키키 값으로 찾으시면 배열이 나옵니다.
```js
"code" :  [ { // 약국의 날짜별 정보
  "date" : "yyyy-MM-dd", // 날짜
  "whenEmpty" : "yyyy-MM-dd HH:mm:ss", // 언제 1개 이하인지
  "whenFew" : "yyyy-MM-dd HH:mm:ss", // 언제 2개 이상 30개 미만인지
  "stock_at" : "yyyy-MM-dd HH:mm:ss", // 입고시간(정부Api)
  "whenSome" : "yyyy-MM-dd HH:mm:ss", // 언제 30개 이상 100개미만인지
  "whenPlenty" : "yyyy-MM-dd HH:mm:ss", // 언제 100개 이상인지(판매 시작? 입고와 동일?)
  "whenBreak" : "yyyy-MM-dd HH:mm:ss" // 언제 판매중지인지
} ]
```
<br>해당 정보를 못 찾을 경우 ""공백으로 제공됩니다.
## 기타
public 라이센스로 사용은 자유롭습니다.
<br>1분마다 수집한 정보를 정리하며 네트워크, 수집 봇의 오류등으로 정밀한 정보를 제공하지는 않습니다. 

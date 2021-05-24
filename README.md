# sm_week12
스마트모바일프로그램설계 12주차

11주차 팀 프로젝트 활동 : https://github.com/Kim-KyungJin/sm_week11

### 팀 구성   
스마트정보통신공학과 201621216 이준석   
스마트정보통신공학과 201921036 김경진   
스마트정보통신공학과 201921054 박유리   
스마트정보통신공학과 201921083 이혜정   
스마트정보통신공학과 201921104 홍수빈    
스마트정보통신공학과 201990009 미르자크메더브 사르더르    

   ***   
### 모든 항목은 변경되거나 삭제될 여지가 있습니다   
   ***   
   
### 파일 합치기 (수빈, 경진, 혜정)
>> 현재 수빈+경진+혜정이 작업하던 파일들은 하나로 통합하였고 추후 유리, 준석, 사르더르의 파일을 합칠 예정입니다. 또한 서로 다른 기능들을 작업했기 때문에 아직 추가 되지 않은 다른 사람의 기능들로의 자유로운 이동을 위해 어플의 전환 흐름을 확인하고 intent를 다음주차에 이어서 작업할 예정입니다. 합치는 과정에서의 버그나 충돌은 현재 작업물까지는 다 해결한 상태라고 파악됩니다. 다만 확인하지 못한 버그나 충돌이 존재할 수 있는데 이 역시 activity, fragment간의 이동을 정리한 후 전체적으로 확인할 예정입니다.
>> 현재는 한 파일로 합쳐져있기는 하지만 전환 기능이 정리 되어 있지 않아, 원활한 화면 전환이 불가능합니다. 지금은 아직 <intent-filter>의 이동을 통한 강제 전환만 가능합니다.
>> 합친 파일은 첨부파일로 추가하기엔 업로드 사이즈를 초과하여, 깃허브 링크를 첨부합니다.
>>  https://github.com/H-Subin/sm_project/tree/combineProJect(0523)



### 해시태그/필터링 (수빈, 유리, 경진)   
>>1. 해시태그(수빈)
>> 해시태그 기능은 한가지 기능문제를 해결한 후 firebase에 연결할 예정입니다. 현재 해시태그를 10개까지로 제한하거나, setting 페이지에서 현재 설정된 해시태그의 개수를 보여주는 등의 문제는 해결 되었지만 이전에 선택되어있던 해시태그들을 체크여부를 불러오는 부분이 미완성입니다. 선택된 해시태그의 gravity 값들을 받아와 하나의 문자열에 담아내는 것까지는 성공하였지만 이를 int형 array로 변경 + 이 array를 이용하며 기존에 체크 되어있던 값들의 boolean값을 강제로 바꿔주는 부분은 조금더 알아보고 완성시킬 예정입니다.
>> 아래는 태그 부분의 실행 영상입니다. 영상 초반에 빈 토스트 창이 나오는 이유는 제가 위에서 말한 아직 해결하지 못한 부분을 해결하기 위해, 일단 임시로 string을 토스트 메시지를 이용하여 값이 잘 담기고 있는지 시각적으로 확인하기 위해 임시로 넣은 부분입니다. 오류가 아니고, 베타 버전이라 아직 토스트로 확인할 필요가 있어 아직 제거하지 않은 것 뿐임으로 버그가 아닙니다. <br>
>> ![20210524_220244](https://user-images.githubusercontent.com/76034369/119352187-53d18880-bcdc-11eb-956c-deecbfb5698b.png)
>>
>>https://user-images.githubusercontent.com/76034369/119354198-be83c380-bcde-11eb-94e7-ebdf9238102a.mp4


### 가게 필터링 (이혜정)
>
>> 1. 가게 필터링
>>
>> 사용자의 위치와 사용자의 검색어로 가게를 필터링하는 기능을 구현했습니다.<br>
>> 우선 위치로 1차 필터링을 합니다. 위치는 상위지역구 하위지역구 두가지로 나뉘며 spinner로 사용자에게 입력받습니다.
>> 상위지역구, 하위지역구 모두 선택되었을 시 db에서 그에 맞는 가게들을 검색하여 필터링합니다.
>> 다음은 db에 필터링하는 부분입니다.

>> ![필터링 부분 코드](https://user-images.githubusercontent.com/79883808/119347649-c50e3d00-bcd6-11eb-9f26-85c1d657a470.PNG)

>> 상위지역구, 하위지역구, 검색어로 총 3번 필터링 되기때문에 코드 중복을 줄이고자 onCreate() 밖에다가 한번에 구현하여 사용했습니다.
>> 각 필터 구분은 db에 검색하려는 key값으로 하였습니다.
>> key 값이 city_string(상위지역구),town_string(하위지역구)일시, db에 사용자가 지정한 지역구와 city_string,town_string의 값과 비교를 진행합니다.
>> 그리고 해당하는 가게들은 for문을 통해 DataSnapshot 형태로 ArrayList에 저장됩니다.
>> 사용할 때는 가게datasnapshot.child()를 이용하여 가게의 이름들과 한줄소개를 불러왔으며 필터링 가게의 이름과 한줄소개가 RecyclerView에 출력되게하였습니다.
>>
>> 검색기능은 지역으로 필터링된 가게에서 필터링되게 하였습니다.
>> 사용자가 입력한 검색어로 시작하는 가게들을 ArrayList에서 찾고 지역 필터링과 마찬가지로 for문을 사용하여 ArrayList에 넣어주었습니다.
>> 마찬가지로 출력도 가게datasnapshot.child()를 이용하여 가게의 이름들과 한줄소개를 불러왔으며 필터링 가게의 이름과 한줄소개가 RecyclerView에 출력되게하였습니다.
>> 다음은 총 실행영상입니다.
  
>> [가게 필터링 실행영상](https://user-images.githubusercontent.com/79883808/119344979-4532a380-bcd3-11eb-9fba-3657caac4242.mp4)


### 인앱광고/유료광고 (사르더르, 준석)  

![Android_Manifest](https://user-images.githubusercontent.com/79889548/119346730-8e83f280-bcd5-11eb-8b57-aa0791ddf193.PNG)

메니페스트 파일에 앱 아이디를 설정해주는 부분입니다. 

![join activity](https://user-images.githubusercontent.com/79889548/119346732-8fb51f80-bcd5-11eb-9770-815762ffc8c5.PNG)

Join Activity 파일에 Adview 설정 및 AdView 광고 초기화 함수 , AdView 사이즈를 정했습니다.
메니페스트 파일과는 다르게 실제 앱 아이디로 하면 광고 화면이 나오는데 오래걸린다고 해서 테스트 아이드로 했습니다. 

![Activity_Join](https://user-images.githubusercontent.com/79889548/119346734-904db600-bcd5-11eb-931e-46babd6002a1.PNG)

AdView 디자인 설정 부분 입니다. 

![Google AdMob](https://user-images.githubusercontent.com/79889548/119346735-904db600-bcd5-11eb-80e9-56f7d4860ad6.PNG)

실행화면 입니다. 


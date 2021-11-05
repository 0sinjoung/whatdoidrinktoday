# What do I drink today project

![iphonex_72](https://user-images.githubusercontent.com/89737184/140475351-95ad6d8b-a51a-4c27-ba65-7f525cf6e7b1.png)


<br/>
<br/>


# What do I drink today
- Personal project
- Term : about 1 week
- Tools : HTML5, CSS3, JavaScript ES6, Vue.js, Git
- Link : https://0sinjoung.github.io/whatdoidrinktoday/

<br/>
<br/>

## 프로젝트 소개

### 💡 아이디어
- 카페에서 주문을 하며 매일 마시는 음료 외에 다른 음료가 마시고 싶을 때 현재 나의 기호를 반영해서 메뉴를 추천해주는 심리 테스트가 있으면 좋겠다는 생각이 들었습니다.
- 카페 고객 입장에서는 음료를 추천받고, 기업 입장에서는 주력 메뉴나 신제품을 홍보할 수 있습니다.
<br/>

### 👤 사용 대상

1. 음료를 추천받고 싶은 카페 고객
2. 신제품 런칭을 홍보하고 싶은 브랜드 담당자
<br/>

### 💁🏻‍♀️ 간략한 소개

- 카페에서 늘 마시던 아메리카노 말고 다른 음료를 마시고 싶다는 생각이 들었을 때, 나의 기호를 반영해서 메뉴를 추천해주는 테스트가 있으면 재밌을 것 같다고 생각이 들어 제작하게 되었습니다.
- MBTI 테스트 유행으로 인해 기업에서 광고로 많이 사용하는 심리테스트 형식으로 제작하였습니다. 상업적으로 사용할 것을 고려하여 제작하였습니다.
- 기업 입장에서는 본인들의 주력 상품 혹은 신제품을 홍보할 수 있는 광고 수단이 될 수 있고, 사용자 입장에서는 간단한 테스트를 통해 음료를 추천받을 수 있습니다.
- 디자인은 매장의 키오스크 UI 느낌을 반영하여 음료를 주문하는 느낌을 살렸고 레트로한 분위기를 낼 수 있는 배경과 색상을 사용했습니다.

<br/>
<br/>

## 주요 기능

### ◾️ 심리테스트와 키오스크 UI/UX
![whatdoi](https://user-images.githubusercontent.com/89737184/140475424-664d1d6f-07b0-4e60-9472-03fb1ed94a4e.png)
- 심리테스트와 음료 매장의 키오스크의 디자인을 차용하였습니다
- 본인의 기호를 선택하여 최종 음료를 주문하는 방식입니다
<br/>

### ◾️ Vue.js 사용

**Vue.js의 장점**

1. 가독성이 높고 직관적
2. 빠르고 안정적인 환경 구축 가능

**Vue.js를 사용한 이유**

1. 동일한 디자인으로 반복되는 질문 리스트를 컴포넌트로 관리
2. 버튼 클릭 이벤트에 따른 user data를 손쉽게 등록, 수정
3. axios를 이용한 데이터 통신
<br/>

### ◾️ User data

```jsx
new Vue({
	el: '#app',
	data: {
		user: {
			name: '',
			brand: '',
      flavor: {
	      hot: true,
        caffein: true,
        milk: true,
        sugar: true
      },
      drinkCode: ''
    }
...
})
```

1. 뷰 인스턴스의 user 데이터는 **name, brand, flavor, drinkCode**를 속성으로 갖습니다
2. 어느 브랜드 매장에서 음료를 마실지 결정하면 해당 값은 **user.brand**에 저장됩니다. user.brand에 저장된 값이 정해지면 다음의 요소가 결정됩니다
    1. footer의 what do I drink today 텍스트 이후에  ‘in 브랜드명’ 요소가 생성됩니다
    2. 브랜드 메인 컬러가 결정됩니다. 브랜드 메인 컬러는 이후 질문 리스트와 결과 페이지의 배경 컬러를 해당 브랜드 컬러로 변경합니다
    3. 결과 페이지에서 불러올 데이터 파일(브랜드명.json)을 결정합니다 
3. **user.name** 속성은 주문자의 이름을 입력하는 input 요소와 연결됩니다
    1. 이름을 입력하지 않으면 주문하기 버튼은 활성화되지 않습니다
    2. 결과 페이지에서 주문자의 이름이 표시됩니다
4. **user.flavor** 속성은 각 질문지에 해당하는 답변을 boolean 값으로 갖습니다
    1. 질문지에 해당하는 버튼을 클릭하면 해당 속성 boolean 값이 변경됩니다
    2. 뒤로가기 버튼을 통해 데이터를 덮어쓸 수 있습니다
5. **user.drinkCode**는 결과보기 버튼을 누르면 생성됩니다
<img width="276" alt="스크린샷 2021-11-05 오후 3 20 33" src="https://user-images.githubusercontent.com/89737184/140475562-374546ec-45f4-49df-a520-f739e79ee39f.png">
<br/>

### ◾️ 음료의 결정

![result72](https://user-images.githubusercontent.com/89737184/140475637-3c8ad4b8-8338-4fdb-9e04-a18dfd3b6339.png)

1. n가지 질문에 따라 Boolean 값을 반환하여 음료를 반환하므로 경우의 수는 n²입니다
2. 질문에 해당하는 음료는 각각 고유 코드를 갖습니다. 고유 코드는 결과보기 버튼을 누르면 user.flavor 데이터를 기반으로 생성됩니다. 값은 user.drinkCode에 저장됩니다
3. user.brand에 저장된 브랜드명에 해당하는 json 파일을 읽어옵니다
4. json 파일에 저장된 code key를 순회하여 user.drinkCode와 동일한 데이터를 찾습니다. 이때 시간 복잡도는 O(n)입니다
5. 해당하는 음료의 정보를 뷰 인스턴스 데이터 selectedDirnk의 값으로 저장하고 결과 페이지를 반환합니다
<br/>

### ◾️ 확장성
![starbucksmocup72](https://user-images.githubusercontent.com/89737184/140475672-dc9341c8-4622-4e57-87ac-f8cc3df38c96.png)

![ediya72](https://user-images.githubusercontent.com/89737184/140475723-0785154d-d755-49c4-a68c-ec43169ab211.png)

1. 각 브랜드의 데이터는 json 파일로 관리됩니다
2. 언제든 다른 브랜드를 추가하여 확장할 수 있습니다
3. user.brand 데이터를 사용해 브랜드 별 메인 컬러를 다르게 적용합니다

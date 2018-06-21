# Please help the jsWarrior to escape in strange corridor!
If you want to help jsWarrior then click [here](http://jswarrior.fusioncharts.com/)!
I will make it possible to escape all the strange corridors with a single code.
Let's help him!

## level1 ~ level7

```JavaScript
jsWarrior.turn = function(warrior) {
  warrior.needRest = warrior.needRest ? warrior.needRest : 8; // 체력 회복 조건이 있으면 그 값을 따르고, 아니면 8로 초기화
  
  if (warrior.check() === 'wall') { // for level7
    warrior.needRest = 20;  // level7에서는 체력이 20이 될때까지 회복하도록 설정
    warrior.goForce = true; // level7에서 달려가다가 JavaLiner에게 맞아도 계속 달려가도록 설정
    warrior.pivot();
  } else if (warrior.check() === 'enemy') { // for all levels
    warrior.attack();
  } else if (warrior.check() === 'diamond') { // for level5
    warrior.collect();
  } else if(!warrior.moveForward) { // for all levels, but especially level6
    if (warrior.check('backward') === 'diamond') {
      warrior.moveForward = true; // 뒤에 있는 다이아를 찾았으면 더이상 뒤로 갈 필요가 없도록 설정
      warrior.goForce = true; // level6에서 달려가다가 JavaLiner에게 맞아도 계속 달려가도록 설정
      warrior.collect('backward');
    } else if (warrior.check('backward') === 'wall') {  // warrior.moveForward 변수는 undefined로 시작하므로 모든 level에서 뒤로 감,
      warrior.moveForward = true; // 이때 벽에 닿으면 더이상 뒤로 안가도록 설정
      warrior.walk();
    } else {
      warrior.walk('backward');
    }
  } else {  // 전진 또는 체력 회복
    if (warrior.getHealth() < 20) {
	    if (warrior.needRest === 8) { // Troll 1마리 또는 JavaLiner 2마리를 상대시 피가 8까지 남음. 
        warrior.needRest = 20;  // 이후부터는 체력이 20까지 회복되도록 설정
        if (warrior.goForce) {  // level6에서 첫 번째 Troll을 잡은 뒤 뒤로 한칸 물러나도록 설정
          warrior.walk('backward');
        } else {
          warrior.walk(); // level4에서 첫 번째 Troll 잡은 뒤 바로 이동해서 JavaLiner에게 다가가도록 설정
        }
      } else if (warrior.getHealth() < warrior.needRest) {  // 실제 체력 회복 부분
        if (warrior.getHealth() === 18 && warrior.goForce) {  // 체력이 18일 경우, 다음 프레임에서 체력이 20으로 증가됨.
          warrior.needRest = 5; // 달려가다가 javaLiner 에게 맞아도 돌진하도록 체력 확인 조건을 낮춤
        }
        warrior.rest();
      } else {
        warrior.walk();
      }
    } else {
      warrior.walk();
    }
  }
}
```
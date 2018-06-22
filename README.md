# Please help the jsWarrior to escape in strange corridor!
If you want to help jsWarrior then click [here](http://jswarrior.fusioncharts.com/)!
I will make it possible to escape all the strange corridors with a single code.
Let's help him!

## level1 ~ level7

```JavaScript
jsWarrior.turn = function(warrior) {
  if (isWallFront(warrior)) {
    warrior.pivot();
  } else if (isBehindSomething(warrior)) {
    handleBackwardDiamond(warrior);
  } else if (readyToFight(warrior)) {
    handleAttack(warrior);
  } else if (isDiamondFront(warrior)) {
    warrior.collect();
  } else if (isUnderAttackFromJavaLiner(warrior)) {
    handleJavaLinerAttack(warrior)
  } else if (isNotHealthy(warrior)) {
    warrior.rest();
  } else {
    warrior.walk();
  }

  saveLastHealth(warrior);
}

function isWallFront(warrior) {
  return warrior.check() === 'wall';
}

function isWallBackward(warrior) {
  return warrior.check('backward') === 'wall';
}

function readyToFight(warrior) {
  return warrior.check() === 'enemy';
}

function isDiamondFront(warrior) {
  return warrior.check() === 'diamond';
}

function isDiamondBackward(warrior) {
  return warrior.check('backward') === 'diamond';
}

function isBehindSomething(warrior) {
  return !warrior.back;
}

function isHaveToRest(warrior) {
  return warrior.getHealth() < 10;
}

function isUnderAttackFromJavaLiner(warrior) {
  return warrior.getHealth() < warrior.health;
}

function isHaveToEscape(warrior) {
  return warrior.getHealth() < 7;
}

function isNotHealthy(warrior) {
  return warrior.getHealth() < 20;
}

function handleBackwardDiamond(warrior) {
  if (isDiamondBackward(warrior)) {
    warrior.back = true;
    warrior.collect('backward');
  } else if (isWallBackward(warrior)) {
    warrior.back = true;
    warrior.walk();
  } else {
    warrior.walk('backward');
  }
}

function handleAttack(warrior) {
  if (isHaveToRest(warrior)) {
    warrior.walk('backward');
  } else {
    warrior.attack();
  }
}

function handleJavaLinerAttack(warrior) {
  if (isHaveToEscape(warrior)) {
    warrior.walk('backward');
  } else {
    warrior.walk();
  }
}

function saveLastHealth(warrior) {
  warrior.health = warrior.getHealth();
}
```
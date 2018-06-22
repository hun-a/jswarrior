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
    if (isDiamondBackward(warrior)) {
      warrior.back = true;
      warrior.collect('backward');
    } else if (isWallBackward(warrior)) {
	    warrior.back = true;
      warrior.walk();
    } else {
      warrior.walk('backward'); 
    }
  } else if (readyToFight(warrior)) {
    if (isHaveToRest(warrior)) {
      warrior.walk('backward');
    } else {
      warrior.attack();
    }
  } else if (isDiamondFront(warrior)) {
    warrior.collect();
  } else {
    if (isUnderAttackFromJavaLiner(warrior)) {
      if (isHaveToEscape(warrior)) {
        warrior.walk('backward');
      } else {
        warrior.walk();
      }
    } else if (isHealthy(warrior)) {
      warrior.rest();
    } else {
      warrior.walk();
    }
  }

  warrior.health = warrior.getHealth();
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
};

function isHaveToEscape(warrior) {
  return warrior.getHealth() < 7;
}

function isHealthy(warrior) {
  return warrior.getHealth() < 20;
}
```
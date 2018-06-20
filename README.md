# Please help the jsWarrior to escape in strange corridor!
If you want to help jsWarrior then click [here](http://jswarrior.fusioncharts.com/)!
I will make it possible to escape all the strange corridors with a single code.
Let's help him!

## level1

```JavaScript
jsWarrior.turn = function(warrior) {
  warrior.walk()
}
```

## level2

```JavaScript
jsWarrior.turn = function(warrior) {
  if(warrior.check() == 'enemy') {
    warrior.attack();
  } else {
    warrior.walk()
  }
}
```

## level3

```JavaScript
jsWarrior.turn = function(warrior) {
  if(warrior.check() == 'enemy') {
    warrior.attack();
  } else if (warrior.getHealth() < 20) {
    warrior.rest();
  } else {
    warrior.walk()
  }
}
```

## level4

```JavaScript
jsWarrior.turn = function(warrior) {
  warrior.needRest = warrior.getHealth() === 20 ? false : warrior.needRest;
  if(warrior.check() === 'enemy') {
    warrior.attack();
  } else {
    if (warrior.getHealth() === 2) {
      warrior.needRest = true;
      warrior.rest();
    } else if (warrior.needRest) {
      warrior.rest();
    } else {
      warrior.walk(); 
    }
  }
}
```

## level5

```JavaScript
jsWarrior.turn = function(warrior) {
  warrior.needRest = warrior.getHealth() === 20 ? false : warrior.needRest;
  if(warrior.check() === 'enemy') {
    warrior.attack();
  } else if (warrior.check() === 'diamond') {
    warrior.collect();
  } else {
    if (warrior.getHealth() === 8) {
      warrior.needRest = true;
      warrior.rest();
    } else if (warrior.needRest) {
      warrior.rest();
    } else {
      warrior.walk(); 
    }
  }
}
```

## level6

```JavaScript
jsWarrior.turn = function(warrior) {
  warrior.moveForward = warrior.moveForward ? warrior.moveForward : false;
  if (warrior.moveForward) {
    if (warrior.check() === 'enemy') {
      warrior.attack(); 
    } else {
      if (warrior.getHealth() === 8 && warrior.moveForward) {
        warrior.moveForward = false;
        warrior.walk('backward');
      } else {
        warrior.walk(); 
      }
    }
  } else {
    if (warrior.check('backward') === 'diamond') {
      warrior.collect('backward'); 
      warrior.moveForward = true;
    } else if (warrior.getHealth() < 20) {
      warrior.rest();
      warrior.moveForward = warrior.getHealth() >= 18 ? true : false;
    } else {
      warrior.walk('backward');
    }
  }
}
```

## level7

```JavaScript
jsWarrior.turn = function(warrior) {
  if(warrior.check() == 'wall') {
    warrior.pivot();
  } else if (warrior.check() === 'enemy') {
    warrior.attack();
  } else if (warrior.getHealth() < 20 && !warrior.isHealthy) {
    warrior.rest();
    warrior.isHealthy = warrior.getHealth() >= 18 ? true : false;
  } else {
    warrior.walk();
  }
}
```
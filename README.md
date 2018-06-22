# Please help the jsWarrior to escape in strange corridor!
If you want to help jsWarrior then click [here](http://jswarrior.fusioncharts.com/)!
I will make it possible to escape all the strange corridors with a single code.
Let's help him!

## level1 ~ level7

```JavaScript
jsWarrior.turn = function(warrior) {
  if (warrior.check() === 'wall') {
    warrior.pivot();
  } else if (!warrior.back) {
    if (warrior.check('backward') === 'diamond') {
      warrior.back = true;
      warrior.collect('backward');
    } else if (warrior.check('backward') === 'wall') {
	  warrior.back = true;
      warrior.walk();
    } else {
      warrior.walk('backward'); 
    }
  } else if (warrior.check() === 'enemy') {
    if (warrior.getHealth() < 10) {
      warrior.walk('backward');
    } else {
      warrior.attack();
    }
  } else if (warrior.check() === 'diamond') {
    warrior.collect();
  } else {
    if (warrior.getHealth() < warrior.health) {
      if (warrior.getHealth() < 7) {
        warrior.walk('backward');
      } else {
        warrior.walk();
      }
    } else if (warrior.getHealth() < 20) {
      warrior.rest();
    } else {
      warrior.walk();
    }
  }

  warrior.health = warrior.getHealth();
}
```
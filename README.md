# Please help the jsWarrior to escape in strange corridor!
If you want to help jsWarrior then click [here](http://jswarrior.fusioncharts.com/)!
I will make it possible to escape all the strange corridors with a single code.
Let's help him!

## level1 ~ level5

```JavaScript
jsWarrior.turn = function(warrior) {
  warrior.needRest = warrior.needRest ? warrior.needRest : 8;
  
  if (warrior.check() === 'diamond') {
    warrior.collect();
  } else if (warrior.check() === 'enemy') {
    warrior.attack();
  } else {
    if (warrior.getHealth() < 20) {
      if (warrior.needRest === 8) {
        warrior.needRest = 20;
        warrior.walk();
      } else if(warrior.getHealth() < warrior.needRest) {
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

## level6 ~ level7 

Need to coding...
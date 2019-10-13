The Jai the syntax of the conditional code execution is similar to other languages but is sometimes terser and simpler.

## If statement
``` cpp
// Jai doesn't require parenthesis to evaluate the condition
if a == b return;
if a > b set_position(p1, p2);
else set_position(p2, p1);

// But it is possible to use parenthesis to combine and 
// control the evaluation order of the conditions
if player.alive && 
  ( player.armor < ARMOR_DEPLETED || player.armor_type == Armor_types.CHAIN_MAIL ){
  player.last_event = Player_event.ARMOR_BROKEN;
}

```
## Else statement
``` cpp
// else statement can run immediately after an if statement
if flag a = 0;
else a = 1;

// or it is possible to use curly braces to create chains of conditions
if monster.is_hit {
  monster.life -= hit_damage;
  if monster.life <= 0 { 
    // increment score
    ...
  } else if monster.life <= ALMOST_DIED {
    // pass in berserker mode
    ...
  } else {
    // seek the player
    ...
  }
}
```
## Switch statement
``` cpp
// In Jai is not available a specific reserved word for conditional branching execution, 
// but it is still possible to use the if statement in the following terse way.

if player.last_event {
  case Player_event.POWERUP_LVL1 play_sound(sound_atlas[Sounds.POWERUP_1]); 
  case Player_event.START_JUMP play_sound(sound_atlas[Sounds.JUMP_1]);
  ... 
  case Player_event.DEATH play_sound(sound_atlas[Sounds.MOAN_TO_DEATH]);
}


```
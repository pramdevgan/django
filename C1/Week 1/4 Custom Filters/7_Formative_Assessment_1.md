# Formative Assessment 1

Drag the code blocks into the box below. Create the filter `oscar_wins`. This filter returns a string that says either the actor has not won an Oscar, or says how many Oscars the actor has won.

**Hint** , not all of the blocks will be used, and the blocks must be properly indented.

Drag from here

* def oscar_wins():
* if oscars == 0:
* @filter

Construct your solution here

* @register.filter
* def oscar_wins(actor):
* if actor.oscars == 0:
* return f"{actor.fist_name} {actor.last_name} has not won an Oscar."
* else:
* return f"{actor.fist_name} {actor.last_name} has won {actor.oscars} Oscars."

Here is the correct answer:

```python
@register.filter
def oscar_wins(actor):
  if actor.oscars == 0:
    return f"{actor.fist_name} {actor.last_name} has not won an Oscar."
  else:
    return f"{actor.fist_name} {actor.last_name} has won {actor.oscars} Oscars."
```

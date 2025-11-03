# ExpNo:10 Implementation of Classical Planning Algorithm
## Name: RAKSHITHA P
## Registration Number: 212223220083
# Algorithm or Steps Involved:
<ol>
  <li>Define the initial state</li>
  <li>Define the goal state</li>
  <li>Define the actions</li>
  <li>Find a <b>plan</b> to reach the goal state</li>
  <li>Print the plan</li>
</ol>

# Example - 1
```
initial_state = {'A': 'Table', 'B': 'Table'}
goal_state = {'A': 'B', 'B': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_Table': {'precondition': {'A': 'Table', 'B': 'B'}, 'effect': {'B': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Output:
```
['move_A_to_B']
```
# Example - 2
```
initial_state = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
goal_state = {'A': 'B', 'B': 'C', 'C': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_C': {'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'}, 'effect': {'B': 'C'}},
    'move_C_to_Table': {'precondition': {'A': 'B', 'B': 'C', 'C': 'C'}, 'effect': {'C': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Output:
```
['move_A_to_B', 'move_B_to_C']
```
## Program:
```
def is_goal_state(current_state, goal_state):
    return current_state == goal_state

def apply_action(current_state, effect):
    new_state = current_state.copy()
    new_state.update(effect)
    return new_state

def is_applicable(current_state, precondition):
    return all(current_state.get(k) == v for k, v in precondition.items())

def find_plan(initial_state, goal_state, actions):
    queue = [(initial_state, [])]
    visited = set()

    while queue:
        state, plan = queue.pop(0)

        if is_goal_state(state, goal_state):
            return plan

        state_key = tuple(sorted(state.items()))
        if state_key in visited:
            continue
        visited.add(state_key)

        for action, details in actions.items():
            if is_applicable(state, details['precondition']):
                next_state = apply_action(state, details['effect'])
                queue.append((next_state, plan + [action]))

    print("No plan exists.")
    return None

initial_state = {'A': 'Table', 'B': 'Table'}
goal_state = {'A': 'B', 'B': 'Table'}
actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_Table': {'precondition': {'A': 'Table', 'B': 'B'}, 'effect': {'B': 'Table'}}
}
plan = find_plan(initial_state, goal_state, actions)
print(plan)

initial_state = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
goal_state = {'A': 'B', 'B': 'C', 'C': 'Table'}
actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_C': {'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'}, 'effect': {'B': 'C'}},
    'move_C_to_Table': {'precondition': {'A': 'B', 'B': 'C', 'C': 'C'}, 'effect': {'C': 'Table'}}
}
plan = find_plan(initial_state, goal_state, actions)
print(plan)

initial_state = {'A': 'Table', 'B': 'Table'}
goal_state = {'A': 'Table', 'B': 'Table'}
actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}}
}
plan = find_plan(initial_state, goal_state, actions)
print(plan)
```

## Output:

<img width="378" height="91" alt="image" src="https://github.com/user-attachments/assets/07e94603-8abd-48ae-95dd-94c0073d5e3b" />

## Result:
Thus the program was executed successfully.

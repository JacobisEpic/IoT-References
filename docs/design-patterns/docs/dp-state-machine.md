# Design Pattern -- State Machine in C

In the following, we assume a simple coffee vending machine that takes
a coin, takes a selection, then dispenses coffee. This is modeled as a
set of states and state transitions wherein states are {idle, coin
inserted, and option selected} and transitions are {insert coin,
select option, coffee ready}. Note the similary of the states of being
vs. the action that caused it to be in a state.

This is illustrated in the state diagram.

<p align="center">
<img src="/docs/images/state1.png" width="100%">
</p>
<p align="center">
<i>State Diagram for Coffee Vending</i>
</p>


The state machine for this problem can be implemented multiple
ways. Here are a few design patterns.

## State machine using conditionals
[From Embedded.com](https://www.embedded.com/design/prototyping-and-development/4442212/Implementing-finite-state-machines-in-embedded-systems)


```c
typdef enum {			// Set of states enumerated
       IDLE_STATE,
       COIN_INSERTED_STATE,
       OPTION_SELECTED_STATE,
       MAX_STATES
       } state_e;

typedef enum {			// Set of events enumerated
	INSERT_COIN_EVENT,
	SELECT_OPTION_EVENT,
	COFFEE_READY_EVENT,
	MAX_EVENTS
	} event_e;

state_e state = IDLE_STATE;	// Starting state
state_e next_state;
event_e event;

while(1)			// When event occurs, event handler does some stuff
{
	event = read_event();
	if (state == IDLE_STATE)
	{
		if (event == INSERT_COIN_EVENT)
		{
			next_state == insert_coin_event_handler();
		}
	else if (state == COIN_INSERTED_STATE)
	{
		if (event == SELECT_OPTION_EVENT)
		{
			next_state == select_option_event_handler();
		}
	else if (state == OPTION_SELECTED_STATE)
	{
		if (event == COFFEE_READY_EVENT)
		{
			next_state == coffee_ready_event_handler();
		}
	}
	state = next_state;
```

## The model above can be implemented as a table comprised of states and events

```c
state_e (*state_table[MAX_STATES][MAX_EVENTS]) (void) = {	// Set up transitions
	{insert_coin_event_handler, error_handler, error_handler},
	{error_handler, select_option_event_handler, error_handler},
	{error_handler, error_handler, coffee_ready_event_handler}
	};

while(1)	// When event occurs, event handler does some stuff
{
	event = read_event();
	if ((event >=0) && (event < MAX_EVENTS))
	{
		nest_state = state_table[state][event]();
		state = next_state;
	}
```


## Another way

```c
#define S0 0		// Define each state
#define S1 1
#define S2 2

void StateMachine(){
     int state = S0; 
     while (1)
     {
     	switch (state)
	{
		S0:
			if (INSERT_COIN) {state = insert_coin_event_handler}
			if (SELECT_OPTION) {state = error_handler}
			if (COFEE_READY) {state = error_handler}
			break;
		S1:
			if (INSERT_COIN) {state = error_handler}
			if (SELECT_OPTION) {state = select_option_handler}
			if (COFEE_READY) {state = error_handler}
			break;
		S2:
			if (INSERT_COIN) {state = error_handler}
			if (SELECT_OPTION) {state = error_handler}
			if (COFEE_READY) {state = coffee_ready_handler}
			break;
	}
     }
}
```


## State machine using two arrays
One for state function pointers and one for state transition
rules. [From Stack
Overflow](https://stackoverflow.com/questions/1371460/state-machines-tutorials)


```c
int entry_state(void);			// Define four states
int foo_state(void);
int bar_state(void);
int exit_state(void);
int (* state[])(void) = { entry_state, foo_state, bar_state, exit_state};
enum state_codes { entry, foo, bar, end};

enum ret_codes {ok, fail, repeat};	// Return codes

struct transition { 	  		// Define the transitions
    enum state_codes src_state;
    enum ret_codes   ret_code;
    enum state_codes dst_state;
};

struct transition state_transitions[] = {	// State transition table
    {entry, ok,     foo},
    {entry, fail,   end},
    {foo,   ok,     bar},
    {foo,   fail,   end},
    {foo,   repeat, foo},
    {bar,   ok,     end},
    {bar,   fail,   end},
    {bar,   repeat, foo}};

#define EXIT_STATE end
#define ENTRY_STATE entry

int main(int argc, char *argv[]) {
    enum state_codes cur_state = ENTRY_STATE;
    enum ret_codes rc;
    int (* state_fun)(void);

    for (;;) {
        state_fun = state[cur_state];
        rc = state_fun();
        if (EXIT_STATE == cur_state)
            break;
        cur_state = lookup_transitions(cur_state, rc);
    }

    return EXIT_SUCCESS;
}

```

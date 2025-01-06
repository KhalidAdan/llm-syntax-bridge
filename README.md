# llm-syntax-bridge

## Data Structures
- Collection of, group of, set of → Arrays/Lists
- Properties of, attributes of → Objects/Maps
- Line of, sequence of → Queues
- Pile of → Stacks

## Flow Control
- As long as, keep doing until → While loops
- For every, taking each → For each loops
- Stop when, exit if → Break
- Skip when, move to next if → Continue
- If, then → If statements
- Otherwise, if not → Else statements

## Functions
- Process for, way to, method of → Function declarations
- Given, using, with → Parameters
- Give back, result is → Return

## Error Handling
- Attempt to → Try
- If it fails then → Catch
- Report error, signal problem → Throw

## Async Operations
- Eventually, when complete → Promise
- Wait for, after → Await

## Examples

### Basic Function
```javascript
// Natural:
"Create a process for checking messages that:
  Given a message
  If message is empty then signal problem
  Otherwise give back true"

// Code:
function checkMessage(message) {
  if (!message) throw new Error()
  return true
}
```

### Async Queue Handler
```javascript
// Natural:
"When a message arrives, if it's marked urgent,
 send it immediately, otherwise add it to the queue"

// Code:
async function handleMessage(message) {
  if (message.isUrgent) {
    await sendMessage(message);
  } else {
    queue.add(message);
  }
}
```

### API Cache Handler
```javascript
// Natural:
"Wait for a user from requireUser
Retrieve if-none-match headers from the request and store them as
Attempt to:
  wait for server cache data from withCache using the EXPLORE_KEY,
  cache object, versionKey of 'gameLibrary' and a callback that
  waits for getGameLibrary as getFreshValue.
  
If the etag matches if-none-match signal problem as web response
with 304 and the same request headers

If not, give back value from dataFn given these inputs:

  first input: results from withCache with eTag property
  second input: object with properties:
    status of 200
    headers from request

If it fails then print and give back the error"

// Code:
async function handler(req) {
  const user = await requireUser();
  const ifNoneMatch = req.headers.get('if-none-match');

  try {
    const { data: cache, eTag } = await withCache({
      key: EXPLORE_KEY,
      cache,
      versionKey: 'gameLibrary',
      getFreshValue: async () => getGameLibrary()
    });

    if (ifNoneMatch && ifNoneMatch === eTag) {
      throw new Response(null, {
        status: 304,
        headers: req.headers
      });
    }

    return dataFn(cache, {
      status: 200,
      headers: req.headers
    });

  } catch (error) {
    console.error(error);
    throw error;
  }
}

// Natural
Create a process for fizzbuzz given a number that:
For every number from 1 to given number:
Attempt to create a result:
- If number splits evenly by 3 and 5, give back 'FizzBuzz'
- Otherwise if number splits evenly by 3, give back 'Fizz'
- Otherwise if number splits evenly by 5, give back 'Buzz'
- Otherwise give back the number itself
Print the result

// Maps to:
function fizzbuzz(num) {
  for (let i = 1; i <= num; i++) {
    let result;
    if (i % 3 === 0 && i % 5 === 0) {
      result = 'FizzBuzz';
    } else if (i % 3 === 0) {
      result = 'Fizz';
    } else if (i % 5 === 0) {
      result = 'Buzz';
    } else {
      result = i;
    }
    console.log(result);
  }
}
```

Console debugging goes much further than just console log - here, we explore...

# console.log()

Most people know console.log(object)
Can also do console.log(msg,values) like sprintf in C or PHP

```
console.log('I like %s but I do not like %s.', 'Skittles', 'M&Ms')
```

will output exactly as you'd expect...

```
I like Skittles but I do not like M&Ms.
```

Common placeholders are %0 for object, %s for string, and %d which is for a decimal or integer.

```
console.log('The state object for %s is %o', "Susan", user)
```

will output the state data for object(user) Susan(string).

# console.dir()

Say you have the following div..

```
<div id='container'>
  <div class="loot 46" data-reactroot>
    <div tabindex="-1">...</div>
      ::after
  </div>
</div>

let element = document.getElementById('container');

console.log(element);
```

console.log(element) will give you just the DOM representation as structured above, however,

```
console.dir(element);
```

will output the element in a more object-like fashion - all the data related to the element vs just the structure.


# console.warn()

Direct replacement for log() is console.warn(). The output is a bit yellow, and a bit more obvious in a cluttered output. The biggest advantage is that you can filter out all the console.log and leave only console.warn. This is particularly helpful in a particularly busy app, clearing the noise can help see your output much more easily.

# console.table()

Intented to display tabular data in a way that's much neater than just dumping out the raw array of objects.

Example of data:

```
const transactions = [{
  id: "7cb1-e041b126-f3b8",
  seller: "WAL0412",
  buyer: "WAL3023",
  price: 203450,
  time: 1539688433
},
{
  id: "1d4c-31f8f14b-1571",
  seller: "WAL0452",
  buyer: "WAL3023",
  price: 348299,
  time: 1539688433
},
{
  id: "b12c-b3adf58f-809f",
  seller: "WAL0012",
  buyer: "WAL2025",
  price: 59240,
  time: 1539688433
}];
```

Console log would output the data like so:

```
▶ (3) [{…}, {…}, {…}]
```

Console.table(data) output everything in a literal table, **very useful**.

The optional second argument is the list of columns you want:

```
console.table(data, ["id", "price"]);
```

Can also sort by columns within the tables, though it can only handle a maximum of 1000 rows of data.

# console.count()

Used for counting - probably not too useful in the real world...

```
for (let i=0; i < 1000; i++) {
  if(i % 2) {
    console.count('odds');
  }
  if(!(i % 5)) {
    console.count('multiplesOfFive');
  }
  if(isPrime(i)) {
    console.count('prime');
  }
}
```

Can reset the counter with console.countReset()

# console.trace()

Useful when you're trying to figure out inside a class or library which caller is causing the problem. For example, there might be 12 different components calling a service, but one of them doesn't have a dependency set up properly.

```
export default class CupcakeService {

  constructor(dataLib) {
    this.dataLib = dataLib;
    if(typeof dataLib !== 'object') {
      console.log(dataLib);
      console.trace();
    }
  }

  ...
}
```

Using console.log() above would tell us what the dataLib is being passed in as, but not where.

# console.time()

This is a better way to track the microtime taken for JS executions.

```
function slowFunction(number) {
  var functionTimeStart = new Date().getTime();
  //something slow or complex with the number
  //factorials, etc
  var functionTime = new Date().getTime() - functionTimeStart;
  console.log('Function time: ${ functionTime }');
}

var start = new Date().getTime();

for (i = 0; i < 100000; i++) {
  slowFunction(i);
}

var time = new Date().getTime() - start;
console.log('Execution time: ${ time }');
```

can be modernized to (no need for any math or temporary variables)

```
const slowFunction = number =>  {
  console.time('slowFunction');
  // something slow or complex with the numbers.
  // Factorials, or whatever.
  console.timeEnd('slowFunction');
}
console.time();

for (i = 0; i < 100000; ++i) {
  slowFunction(i);
}
console.timeEnd();
```

# console.group()

Allows one to group/nest things; excels in showing structure that exists in code.

```
// this is the global scope
let number = 1;

console.group('OutsideLoop');
console.log(number);
console.group('Loop');

for (let i = 0; i < 5; i++) {
  number = i + number;
  console.log(number);
}

console.groupEnd();
console.log(number);
console.groupEnd();
console.log('All done now');
```

Useful to make clear the context of your logging.

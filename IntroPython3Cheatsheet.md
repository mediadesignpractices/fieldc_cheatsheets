DATA TYPE
========

### Strings

|             | Example   |
| ----------- |:----------:|
| **Correct**     | `a = ‘test’` or `a = “test”` |
| **Incorrect**   | `a = test` |

***

### Integers/Floats

|             | Example   |
| -----------|:----------:|
| **Integer** | `a = 5`  |
| **Float**   | `a = 5.0` |

---

### Lists

|             | Example   |
| -----------|:----------:|
| **Declaration** | `h = [‘this’, ‘is’, ‘a’, ‘list’]`  |

**Add an Element**

|             | Example   |
| -----------|:----------:|
| **insert**(index,'value')   | `h.insert(3,  ‘great’)` |
| **append**('value')   | `h.append(‘certainty’)` |


**Remove an Element**

|             | Example   | Output |
| ---------- |:----------:|:-------:|
| **remove()**   | `h.remove('is')` | removes the value |
| **pop()**| `h.pop()`|`'List'`


**More functions and commands**

|             | Example   | Output |
| -----------|:----------:|:------:|
| **_h[:'value']_**   | `h[:2]` | `['this','is']`
| **_length_**| `len(h)`| `4`|
|**_index()_**| `h.index('this')`| `1`


---

### Dictionaries

|             | Example   |
| -----------|:----------:|
| **Declaration** | `d={‘name’:’boris’,'age':40, 'hair':'bald'}`  |

**Add a new key-value**

|             | Example   | output
| -----------|:----------:|:------:|
| **d['Key'] = 'Value'**   | `d [‘eyes’ ]= ‘brown’` | randomly added

**Delete an item from the dictionary by key**

|             | Example   | output
| -----------|:----------:|:------:|
| **del()**   | `del d['age']` | deletes the key and value
| **pop()**   | `d.pop(‘name’)` |`boris`|

---

### Convert Datatypes

> a = 5

> b = 3.4


| | Example| Output
|---|---|---|
|**integer** to **float**| `float(a)`| a = 5.0
|**float** to **Integer**|`int(b)`|b = 3

---

Loop functions
========

### If Statements

If statements use boolean logic i.e (**true** or **false**).

#### Example : prompt a user response

_input_
>x = int( input(' _please enter an integer:_ ') )  

>if x < 0: >

>> x = 0 

>>print( '_negative changed to zero_') 

>elif x == 0: 
>>print( '_Zero_') 

>elif x == 1:
>>print('_single_')

>else:

>>print('_more_')

### For statements
#### Example : iterate a list

_Input_
>list = ['a',2,'b','d']
>
for `index` in list: `'index' is a temporary variable which stores the elements of the list`
>>print(index)

_Output:_ a 2 b d

---

Other Functions
=======
### Range function

The range function makes a list of arithmetic progression.

|             | Example   | output
| -----------|:----------:|:----:|
| **range()** | `range(10)`  |range(0,10)

_input_
>range(10)

_output_
> range(0,10)


# How to list out all the numbers in between 0 and a?

>range(a) = [0, a]

# How to get a list of all numeric values between 2 numbers?

>range (a, b) = [a, b]

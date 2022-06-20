# Debugging PHP
Learning challenge on how to debug php with Xdebug

## Learning Objectives
- understanding the root of bug fixing
- know what print_r, var_dump, die, echo, exit, break do
- know what to do the next time you're stuck
- give yourself the `solver's mentality`, a problem is just an opportunity to learn!

## Debugging Exercises

You can find the debugged version in the [expert.php](https://github.com/z3no/php-debugging/blob/main/expert.php) file

### Exercise 1

```
echo "Exercise 1 starts here:";

function new_exercise() {
    $block = "<br/><hr/><br/><br/>Exercise $x starts here:<br/>";
    echo $block;

}
```
In the first exercise the variable $x isn't defined. This gave us an error.

### Exercise 2

```
new_exercise(2);
// Below we create a week array with all days of the week.
// We then try to print the first day which is monday, execute the code and see what happens.
$week = ["monday", "tuesday", "wednesday", "thursday", "friday", "saturday", "sunday"];
$monday = $week[1];

echo $monday;
```
The index number of the array is set to 1, which is equal to tuesday.

### Exercise 3

```
new_exercise(3);
// This should echo ` "Debugged !" `, fix it so that that is the literal text echo'ed

$str = “Debugged ! Also very fun”;
echo substr($str, 0, 10);
```
Looked up information about strings [here](https://www.php.net/manual/en/language.types.string.php) and information about [substr](https://www.php.net/manual/en/function.substr.php)

### Exercise 4

```
new_exercise(4);
// Sometimes debugging code is just like looking up code and syntax...
// The print_r($week) should give:  Array ( [0] => mon [1] => tues [2] => wednes [3] => thurs [4] => fri [5] => satur [6] => sun )
// Look up whats going wrong with this code, and then fix it, with ONE CHARACTER!

foreach($week as $day) {
    $day = substr($day, 0, strlen($day)-3);
}

print_r($week);
```

Information about [foreach](https://www.php.net/manual/en/control-structures.foreach.php).
In order to be able to directly modify array elements within the loop precede $value with &. In that case the value will be assigned by reference.

### Exercise 5

```
new_exercise(5);
// The array should be printing every letter of the alfabet (a-z) but instead it does that + aa-yz
// Fix the code so the for loop only pushes a-z in the array

$arr = [];
for ($letter = 'a'; $letter <= 'z'; $letter++) {
    array_push($arr, $letter);
}

print_r($arr); // Array ([0] => a, [1] => b, [2] => c, ...) a-z alfabetical array
```

Information about [range](https://www.php.net/manual/en/function.range.php)
Range creates an array containing a range of elements in our case from 'a' to 'z'.

### Exercise 6

```
new_exercise(6);
// The fixed code should echo the following at the bottom:
// Here is the name: $name - $name2
// $name variables are decided as seen in the code, fix all the bugs whilst keeping the functionality!
$arr = [];


function combineNames($str1 = "", $str2 = "") {
    $params = [$str1, $str2];
    foreach($params as $param) {
        if ($param == "") {
            $param = randomHeroName();
        }
    }
    echo implode($params, " - ");
}


function randomGenerate($arr, $amount) {
    for ($i = $amount; $i > 0; $i--) {
        array_push($arr, randomHeroName());
    }

    return $amount;
}

function randomHeroName()
{
    $hero_firstnames = ["captain", "doctor", "iron", "Hank", "ant", "Wasp", "the", "Hawk", "Spider", "Black", "Carol"];
    $hero_lastnames = ["America", "Strange", "man", "Pym", "girl", "hulk", "eye", "widow", "panther", "daredevil", "marvel"]
    $heroes = [$hero_firstnames, $hero_lastnames];
    $randname = $heroes[rand(0,count($heroes))][rand(0, 10)];

    echo $randname;
}

echo "Here is the name: " . combineNames();
```

Having a lot of troubles with this one, I get some value but it's not what we want. At the moment I'm getting an array value of the firstnames - lastnames (value).
We actually need a random firstname and lastname together then the ' - ' and another random firstname with a random lastname.
I'm not seeing it so I'll focus myself on the next exercises.

### Exercise 7

```
new_exercise(7);
function copyright(int $year) {
    return "&copy; $year BeCode";
}
//print the copyright
copyright(date('Y'));
```

To solve this one I found information on how to work with [dates](https://www.php.net/manual/en/function.date.php).
I also changed the int to a string.

### Exercise 8

```
new_exercise(8);
function login(string $email, string $password) {
    if($email == 'john@example.be' || $password == 'pocahontas') {
        return 'Welcome John';
        return ' Smith';
    }
    return 'No access';
}

//do not change anything below
//should great the user with his full name (John Smith)
echo login('john@example.be', 'pocahontas');
//no access
echo login('john@example.be', 'dfgidfgdfg');
//no access
echo login('wrong@example.be', 'wrong');
//you can change things again!
```

It is not possible to return multiple values in php it will stop at the first return.
You can put the values you want to output in array. I just added the last name to the first return.
I took a look at the [logical operators](https://www.php.net/manual/en/language.operators.logical.php) in php and changed the || OR operator to && AND.

### Exercise 9

```
new_exercise(9);
function isLinkValid(string $link) {
    $unacceptables = array('https:','.doc','.pdf', '.jpg', '.jpeg', '.gif', '.bmp', '.png');

    foreach ($unacceptables as $unacceptable) {
        if (strpos($link, $unacceptable) == true) {
            return 'Unacceptable Found<br />';
        }
    }
    return 'Acceptable<br />';
}
//invalid link
isLinkValid('http://www.google.com/hack.pdf');
//invalid link
isLinkValid('https://google.com');
//VALID link
isLinkValid('http://google.com');
//VALID link
isLinkValid('http://google.com/test.txt');
```

I looked at the information I could find about [strpos](https://www.php.net/manual/en/function.strpos.php).
There I found the following:
`To know that a substring is present (in any position including 0), you can use either of:
!== FALSE (recommended) or > -1 (note: or greater than any negative number)`

### Exercise 10

```
new_exercise(10);

//Filter the array $areTheseFruits to only contain valid fruits
//do not change the arrays itself
$areTheseFruits = ['apple', 'bear', 'beef', 'banana', 'cherry', 'tomato', 'car'];
$validFruits = ['apple', 'pear', 'banana', 'cherry', 'tomato'];
//from here on you can change the code
for($i=0; $i <= count($areTheseFruits); $i++) {
    if(!in_array($areTheseFruits[$i], $validFruits)) {
        unset($areTheseFruits[$i]);
    }
}
var_dump($areTheseFruits);//do not change this
```

To solve the last one I found some good information at the following [link](https://electrictoolbox.com/php-for-loop-counting-array/).
This helped me solve the exercise.
# Technical Assessment Questions

## Question 1

Write code in your preferred OOP language that models an abstract filesystem: 

```
* directoryA (Root)
	* fileA.jpg
	* directoryB
		* fileB.txt
		* fileC.txt
		* directoryC
			* fileD.jpg
	...
```

The code should support creating, deleting, and retrieving items from this modeled filesystem. The filesystem has a single top-level (root) directory under which all other directories and files must be nested. Each directory within the filesystem has a unique name and may have nested directories and/or files. Each file within a directory likewise has a unique name.

### Your code should support the following operations:

- *Adding a directory to the filesystem*
	- When adding a directory to the filesystem, a name and the parent directory name should be specified.
	- If `null` is specified as the parent directory name, the directory is the root directory.
	- If `null` is specified as the parent directory name and a root directory already exists, an exception is thrown.
	- If a directory with the same name already exists, an exception is thrown.
	- If a parent directory name is specified but does not exist, an exception is thrown.
	
- *Adding a file to a directory*
	- When adding a file to a directory, a file name and the parent directory name should be specified.
	- If a file with the same name already exists in that directory, an exception is thrown.
	- If a directory name is specified but does not exist in the filesystem, an exception is thrown.
	
- *Retrieving a directory's direct items*
	- When retrieving a directory's direct items (e.g., it's nested directories and files), the name of the parent directory whose direct items you want to retrieve should be specified. The operation should return a list of file and subdirectory names.
	- If the specified parent directory does not exist, return an empty list.
	- Note that you do not need to return all nested items from a parent directory, but rather only its *direct* children.
  
- *Deleting a file*
	- When deleting a file, a file name and parent directory name should be specified.
	- If the file name does not exist in the specified parent directory, an exception is thrown.

- *Deleting a directory*
	- When deleting a directory, a directory name should be specified.
	- If the directory name does not exist, an exception is thrown.
	- Deleting a parent directory should delete all items nested under that directory.

*Example:*

`$f = new Filesystem;`

`$f->addDirectory('directoryA', null);` // creates a root directory 'directoryA'

`$f->addFile('fileA.jpg', 'directoryA');` // adds 'fileA.jpg' to 'directoryA'

`$f->addDirectory('directoryB', 'directoryA');` // adds 'directoryB' nested under 'directoryA'

`$f->addFile('fileB.txt', 'directoryB');` // adds 'fileB.txt' to 'directoryB'

`$f->addFile('fileC.txt', 'directoryB');` // adds 'fileC.txt' to 'directoryB'

`$f->addDirectory('directoryC', 'directoryB');` // adds 'directoryC' nested under 'directoryB'

`$f->addFile('fileD.jpg', 'directoryC');` // adds 'fileD.jpg' to 'directoryC'

`echo implode(', ', $f->getItems('directoryA'));` // 'directoryB', 'fileB.txt', 'fileC.txt'

`$f->deleteSubdirectory('directoryB');` // the filesystem contains only 'directoryA' with a single file 'fileA.jpg'

`$f->deleteFile('directoryA', 'fileA.jpg');` // the filesystem contains the empty directory, 'directoryA'

## Question 2

Using what you know about object-oriented programming, write the necessary classes in your preferred OOP language to model the following scenario:

- Chickens are one of many types of birds.
- All birds, including chickens, have a `layEgg` behavior.
- The `layEgg` behavior for a given bird produces a new egg.
- An egg can be one of many types -- `chickenEgg`, `turkeyEgg`, etc. 
- All eggs, including chicken eggs, have a `hatch` behavior.
- An egg can only hatch once and will always produce a bird of the appropriate type.

## Question 3

Write a function that will take a string `str` and an array `shifts`, where `shifts[i] = [the shift direction, the shift amount]`. The shift direction will either be the integer `0` for a left shift or the integer `1` for a right shift. The shift amount will be an integer representing the number of positions to shift the letter in the string. 

Note that a left shift of `1` means that you should remove the first letter from the string and append it to the end. Likewise, a right shift of `1` means that you should remove the last letter of the string and add it to the beginning.

Assume the string has a length of under `1000` lowercase English letters, the shift direction is always one of `0` or `1`, and the shift amount will always be between `1` and `1000`.

The function should return the shifted string.

*Example #1*

Input: 
`$str = "xyz"`, `$shifts = [[0,1],[1,2]]`

Output: 
`"zxy"`

Explanation: 
- `[0,1]` means shift the string left by `1`. The new string is `"yzx"`.
- `[1,2]` means shift the string right by `2`. The new string is `"zxy"`.

*Example #2*

Input: 
`$str = "abcdefg"`, `$shifts = [[1,1],[1,1],[0,2],[1,3]]`

Output: 
`"efgabcd"`

Explanation: 
- `[1,1]` means shift the string right by `1`. The new string is `"gabcdef"`.
- `[1,1]` means shift the string right by `1`. The new string is `"fgabcde"`.
- `[0,2]` means shift the string left by `2`. The new string is `"abcdefg"`.
- `[1,3]` means shift the string right by `3`. The new string is `"efgabcd"`.

# Question 4

Assume we have a database with two tables -- `customer_service_representatives` and `customer_service_tickets`. 

`customer_service_representatives`
| id | name |
|---|---|
| 1 | Zack Morris |
| 2 | Lisa Turtle |
| 3 | Kelly Kapowski |
| 4 | A.C. Slater |
| ... | ... |

`customer_service_tickets`
| id | customer_id | customer_service_representative_id | status | description |
|---|---|---|---|---|
| 1 | 1000 | 2 | 1 | Bacon ipsum dolor amet shoulder ham spare ribs kielbasa bacon shankle biltong. |
| 2 | 857 |  3 | 0 | Pork loin jerky brisket chicken biltong, spare ribs cow tongue sirloin ground round tail. |
| 3 | 454 |  3 | 1 | Turducken ham hock tri-tip shankle jerky bresaola flank. |
| ... | ... | ... | ... | ... |

Each ticket in `customer_service_tickets` has a foreign key, `customer_service_representative_id`, corresponding to the `id` column in `customer_service_representatives`. Write a query that returns the following data for each representative: the representative's id, the representative's name, and the total number of tickets associated with that representative.

# UTILS3

Python Helpers and utilities for Functional Programming in Python compatilbe with Python 3 and Python 2.7.

This modules provides the following submodules:

   * **Chain**         Chain class that is useful for piping, sequencial functional programming. Similar to Fsharp, Scala and Ruby.
   
   * **Path**          Fast and Syntax sugar Path Manipulation to write path operations in pipeline and in sequence.
   
      
   * **Enum**          Enumeration Type Class/ Similar to C ENUM
   
   * **Container**     A Generalized dot dictionary
   
   * **hof**          A collections of Higher Order Functions and functions for list and sequence processing based on functional 
                      programming languages like Haskell, Fsharp, Ocaml and Ruby.
   
   * **windows**      Windows OS Helpers for Python.
   
   * **check**       Functions to test variable type,, test operating system and python version.

# MODULES


## Enum


```python

>>> colors = Enum(["blue", "red", "white", "green", "yellow"])
>>> colors
blue = 0, red = 1, white = 2, green = 3, yellow = 4
>>> 
>>> colors.blue
0
>>> colors.red
1
>>> colors.green
3
>>> 
>>> colors.name(1)
'red'
>>> colors.name(2)
'white'
>>> colors.name(3)
'green'
>>> 


```


## Container 



## Path


Examples:


#### Especial Directories

```python
    
>>> from utils3 import Path

>>> # Get current Directory Path
... 
>>> Path.pwd()
/home/tux
>>> 


>>> # Get Home directory
... 
>>> Path.home()
/home/tux
>>> 
>>>

>>> # Get the directory where the script(calling) is located equivalent to __file__
... 
>>> Path.here()
/home/tux/<stdin>
>>> 

>>> # Current Python runtime Path
... 
>>> Path.executable()
/usr/bin/python3c
>>>

```

#### Path Concatenation

```python
    
>>> from utils3 import Path

>>> # Concatenate Paths using the Slash operator
... 
>>> Path.home() / "Downloads" 
/home/tux/Downloads
>>> 

>>> Path.home().get("xen")
/home/tux/xen
    
```

#### Listing Directories

```python
    
>>> from utils3 import Path

>>> # Listing Directories
...
>>> Path.home().get("xen").list()
['owned.jpg', 'network.sh', 'associacao-brasileira-de-normas-tecnicas-ufsm-alfa.csl', 'win7']
>>> 


>>> # List directory with absolute Path
...
>>> Path.home().get("xen").list(1)
['/home/tux/xen/owned.jpg', '/home/tux/xen/network.sh', '/home/tux/xen/associacao-brasileira-de-normas-tecnicas-ufsm-alfa.csl', '/home/tux/xen/win7']
>>> 

>>> # List only directories
... 
>>> Path.home().get("xen").list_dirs()
['win7']
>>> 

>>> # List only files
... 
>>> Path.home().get("xen").list_files()
['owned.jpg', 'network.sh', 'associacao-brasileira-de-normas-tecnicas-ufsm-alfa.csl']
>>> 

>>> # Newest File in Directory 
... 
>>> 
>>> downloads = Path.home().get("Downloads")
>>> 
>>> downloads.newest()
/home/tux/Downloads/mongodb-linux-i686-2.6.7
>>> 
>>> downloads.newest().path
'/home/tux/Downloads/mongodb-linux-i686-2.6.7'
>>> 


>>> # Wak Directory 
... 
>>>  Path.home().get("xen").walk()
['/home/tux/xen/owned.jpg', '/home/tux/xen/network.sh', '/home/tux/xen/associacao-brasileira-de-normas-tecnicas-ufsm-alfa.csl', '/home/tux/xen/win7/win7.cfg', '/home/tux/xen/win7/fullscreen.sh', '/home/tux/xen/win7/win7.sh', '/home/tux/xen/win7/win7.img', '/home/tux/xen/win7/README.txt', '/home/tux/xen/win7/.geanyprj', '/home/tux/xen/win7/desktop.sh']
>>> 

>>> # Enter in directory or path
... 
>>> Path.home().get("xen").cd()
>>> 
>>> os.getcwd()
'/home/tux/xen'
>>> 


>>> # Get Parent Directory
... 
>>> xen = Path.home().get("xen")
>>> xen.top
/home/tux
>>> 
>>> xen.top.top
/home
>>> xen.top.top.top
/
>>>
    
```

### Testing Files

```python

>>> # Test if it is file, directory of if it exists
... 
>>> 
>>> xen =  Path.home().get("xen")
>>> 
>>> xen.path
'/home/tux/xen'
>>>

>>> xen.is_file()
False
>>>

>>> xen.is_dir()
True
>>> 

>>> 
>>> fp = xen.get("network.sh")
>>> 
>>> fp.path
'/home/tux/xen/network.sh'

>>> fp.is_file()
True
>>> fp.is_dir()
False
>>> 
>>> fp.exists()
True
>>> 
>>> 

>>> # Test if File is in directory
... 
>>> 'network' in xen
False
>>> 'network.sh' in xen
True
>>> 
>>> 


>>> # Get file Basename (file name without path)
... 
>>> fp.name
'network.sh'
>>> 

>>> # Get file directory
... 
>>> fp.dir
/home/tux/xen
>>> # Get file Extension
... 
>>> fp.ext
'.sh'
>>> 
>>> # Get file top diretory
... 
>>> fp.dir.top
/home/tux
>>> 
>>> 

>>> # Modification Time
>>> fp.mtime(1)             
'Fri Oct  3 00:53:51 2014'
>>> 
>>> fp.mtime(0)         # Unix Timestamp
1412308431.4800513


>>> # Get file size
... 
>>> fp.size()
190
>>> 

>>> # File MD5 sum
... 
>>> fp.md5()
'7481e37d0a0cce49f0515cd963e0f361'
>>> 

>>> # Reading Files
... 
>>> fp.read()
'echo 1 > /proc/sys/net/ipv4/ip_forward\niptables -t nat -A POSTROUTING -o wlan3 -j MASQUERADE\nifconfig xenbr0 10.0.0.1\nifconfig xenbr0 netmask 255.255.0.0\nsudo xm client /home/tux/xenwin7.cfg'
>>> 
>>> 

>>> # Get File Permissions - Only works on UNIX like systems
...
>>> fp.owner()
'tux'
>>> fp.group()
'tux'
>>> fp.perms()
['rw-', 'rw-', 'r--']
>>> fp.perms(1)
[6, 6, 4]
>>> 
>>> fp.gid()
1000
>>> fp.uid()
1000
>>> 
>>> fp.perms()
['rw-', 'rw-', 'r--']
>>> 

>>> fp.info()
Path : /home/tux/xen/network.sh

Modification Time : Fri Oct  3 00:53:51 2014


Owner:  tux - Uid:  1000
Group:  tux - Gid:  1000

Permissions: 664
	Owner: rw-	Group: rw-	Others: r--


Size: 0.185546875 Megabytes
>>> 

```

### Compressed Files


```python


>>> # Working with Compressed files
... 
>>> fp = Path.home() / "Downloads" / "Luhn_algor1946601162005.zip"
>>> fp
/home/tux/Downloads/Luhn_algor1946601162005.zip

>>> fp.is_zip()
True
>>> 
>>> fp.is_tar()
False
>>> 

>>> # List Compressed file content
...    
>>> fp.list_archive()
['@PSC_ReadMe_63180_1.txt', 'basCalculation.bas', 'frmMain.frm', 'frmMain.frx', 'kid.ico', 'KID.vbp']
>>> 

>>> # Extract Compressed File
...
>>> out = fp.extract("/tmp/content")
>>>
>>> out
/tmp/content
>>> out.list()
['@PSC_ReadMe_63180_1.txt', 'kid.ico', 'frmMain.frx', 'basCalculation.bas', 'KID.vbp', 'frmMain.frm']
>>> 
>>> 

>>> # Remove directory
... 
>>> out.rm()
True
>>> 
>>> # Remove
... 
>>> out.is_dir()
False
>>> 
 


```

## Chain

Examples:

```python

>>> from utils3 import Chain
>>>
>>> x = Chain([['233', 'a', 'b'], ['4343', 'y', 'o'], ['44', 'p', 'k']])

>>>
>>> x
Chain : [['233', 'a', 'b'], ['4343', 'y', 'o'], ['44', 'p', 'k']]
>>>

Test if Chain is empty
>>> x.is_empty()
False

Flat All sublists
>>> x.flat()
Chain : ['233', 'a', 'b', '4343', 'y', 'o', '44', 'p', 'k']

Get an Element by Position
>>> x[0]
['233', 'a', 'b']
>>> x[1]
['4343', 'y', 'o']

Count the Number of Elements
>>> x.count()
3

Get an Element of each sublist by postion in this list
>>> x.select_pos(0)             # Get the element 0 in each sublist
Chain : ['233', '4343', '44']
>>> x.select_pos(1)             # Get the element 1 in each sublist
Chain : ['a', 'y', 'p']
>>> x.select_pos(2)
Chain : ['b', 'o', 'k']
>>> x.select_pos(3)
Chain : [None, None, None]


>>> x.enumerate()
Chain : [(0, ['233', 'a', 'b']), (1, ['4343', 'y', 'o']), (2, ['44', 'p', 'k'])]

Add a New Element to the list
>>> x.append(['1669', 'u', 'k'])
Chain : [['233', 'a', 'b'], ['4343', 'y', 'o'], ['44', 'p', 'k'], ['1669', 'u', 'k']]


Reversing a list, creates a new list
>>> x.reverse()
Chain : [['44', 'p', 'k'], ['4343', 'y', 'o'], ['233', 'a', 'b']]

Retrive the Original Data
>>> x.list
[['233', 'a', 'b'], ['4343', 'y', 'o'], ['44', 'p', 'k']]


Converting a sequence of strings to Int
>>> x.select_pos(0).to_int()
Chain : [233, 4343, 44]

>>> x.select_pos(0).to_int().list
[233, 4343, 44]

>>> x.select_pos(0).to_float().list
[233, 4343, 44]

>>> x.update_pos(lambda x: float(x)/10, 0)
Chain : [[23.3, 'a', 'b'], [434.3, 'y', 'o'], [4.4, 'p', 'k']]
>>>

>>> y = x.update_pos(lambda x: float(x)/10 -1, 0)
>>> y
Chain : [[22.3, 'a', 'b'], [433.3, 'y', 'o'], [3.4000000000000004, 'p', 'k']]


>>> y.select_by_pos(lambda x: x > 20, 0)
[[22.3, 'a', 'b'], [433.3, 'y', 'o']]
>>>

>>> y.select_by_pos(lambda x: x<10, 0)
[[3.4000000000000004, 'p', 'k']]
>>>

>>> y.select_by_pos(lambda x: x == 'a', 1)
[[22.3, 'a', 'b']]
>>>

```


  
   


#### Daylen Haines
#### November 18, 2019
#### Foundations of Programming:  Python
#### Assignment 07

# Python – Pickling and Structured Error Handling

## Introduction
In this document, I will describe what Pickling and Structured Error Handling are in Python, how they can be used in programing, the benefits they provide, and share some example scripts.  This document provides the steps I took and can serve as a guidance for beginning programmers writing or modifying a script with functions.  

## Pickling
Pickling or pickle in Python allows you to convert a python object (list, dict, etc.) into a character stream (Binary).  The idea is that this character stream contains all the information necessary to reconstruct the object in another Python script (https://pythontips.com/2013/08/02/what-is-pickle-in-python/. Nov 2019) (External Site).  Pickled files must be stored as binary files (text files will not work, no .txt) and as such, there are different access methods we need to be familiar with.  Below is a list of the common binary access files utilized in Python (Table 1.1) (Dawson M., Python Programming For The Absolute Beginner. Course Technology, 2010).  

![Table1.1](https://github.com/dhaines44/ITFnd100-Mod07/blob/master/docs/Table1.1-Assignment07.png "Table 1.1")
Table 1.1
                                                      
When creating or accessing a large data set, we will need to write (“wb”) a binary file (.dat) that we can dump our data set into.  With pickling the way to load data into an identified list, dictionary, etc. is through the use of the pickle.dump function() (Figure 3.0).  Pickle.dump(object, file, [.bin]) writes pickled version of object to file. If bin is True, object is written in binary format.  If bin is False, object is written in less efficient, but more human –readable.text format.  The default value of bin is equal to false (Dawson M., Python Programming For The Absolute Beginner. Course Technology, 2010).  Once we have written or dumped the data into our .dat file, we need to close the file so we can move onto our next step of accessing the data. (If we had chosen to append a pre-existing dictionary, list, etc. we could utilize the “ab” or append binary file to ensure we keep the original content of the dictionary, list, etc.(Figure 3.3)).

To access or retrieve the data that was written or appended thorugh the pickle.dump function, we need to write a new script utilizing the pickle.load () function (Figure 3.0). Since we are only interested in reading what was in the given .dat file, we utilize the “rb” or read from binary mode .  Pickle.load(file) unpickles and returns the next pickled object in the file (Dawson M., Python Programming For The Absolute Beginner. Course Technology, 2010).  Once we unpickle our desired .dat file, we need to close the function on the script.  
Now that we have enabled our script to read the chosen binary file (.dat), we can show the contents of the file through the print() function.  With the print function you can return the entire list or select specific items in the list (Figure 3.0).  
 Pickling is most effective with large data sets.  Utilizing pickling to access large dictionaries or data sets from servers or other files can increase data import speeds by 50 to 100 times, making your script easier to run.  A warning with pickling is that pickling is not encrypted and it does not protect against erroneous or maliciously constructed data.  Never unpickle data received from an untrusted or unauthenticated source.  If you were to unpickle data that had a virus in it, you could put your computer at risk of an attack.  Pickling is also very effective If you are reading data from source online, need to clean up data and, unpack the data.  Once you have the data cleaned, you can pickle the data so you can reference or use it at a later time in your script(Mark Jay. Pickling Data with Python! https://www.youtube.com/watch?v=Pl4Hp8qwwes&feature=emb_rel_pause. Nov 2019) (External Site).
```
# --------------------------------------------------#
# Title:  Assignement07 - Pickling
# Dev:  DHaines
# Date:  Nov 19, 2019
# ChangeLog:  (Who, When, What)
#   DHaines, 11/19/2019, Created Script
# --------------------------------------------------#

import pickle # imports code from another file
print("Grocery List\n") # print Grocery List so the User knows what they are looking at

# Data ----------------------------------------------------------------------------------#
strGL = "GroceryList.dat" #Grocery List dictionary
lstItems = ["apples", "bananas", "avacados", "spinach", "broccoli", "carrots", "ground turkey", "chicken breast", "pasta", "eggs"]# Grocery List Items

# Processing ----------------------------------------------------------------------------#
#Open Grocery List in Python
gl = open("GroceryList.dat", "wb")# Write Grocery List data into GroceryList.dat (wb = write binary)
pickle.dump(lstItems, gl) # pickle.dump() function, writes pickled version of object to file
gl.close() # closes gl file

# Unpickle and read Grocery List data
gl = open("GroceryList.dat","rb") # gl = open("GroceryList.dat", rb = read binary)
lstItems = pickle.load(gl) # pickle.load() function, unpickles and returns object written to file. Only returns one row of data
gl.close() # closes gl file

# Presentation ----------------------------------------------------------------------------#
# Showing Grocery List
print(lstItems) # prints items in list
print("\n",lstItems[0],lstItems[1], lstItems[2])
gl.close() # closes gl file

input("\n\n Press Enter Key to Exit.")
```
Figure 3.0 - Pickling With "wb" Write Binary and "rb" Read Binary

![Figure 3.1](https://github.com/dhaines44/ITFnd100-Mod07/blob/master/docs/Figure3.1-Assignment07.png "Figure 3.1")
Figure 3.1 - Pickling With "wb" Write Binary and "rb" Read Binary PyCharm Interactive Results
![Figure 3.2](https://github.com/dhaines44/ITFnd100-Mod07/blob/master/docs/Figure3.2-Assignment07.png "Figure 3.2")
Figure 3.2 - Binary GroceryList.dat Notepad

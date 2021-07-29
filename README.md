# Iterables and Iterators

## Assignment
- Assignment is as below.
    - Goal 1:
        - Refactor the `Polygon` class so that all the calculated properties are lazy properties, i.e. they should still be calculated properties, but they should not have to get recalculated more than once (since we made our `Polygon` class "immutable").
    - Goal 2:
        - Refactor the `Polygons` (sequence) type, into an **iterable**. Make sure also that the elements in the iterator are computed lazily - i.e. you can no longer use a list as an underlying storage mechanism for your polygons.You'll need to implement both an iterable and an iterator.

## Assignment Solution

- File that holds required functions for part 1: Polygon.py
- Github Location : https://github.com/anilbhatt1/epai_3_p1_s12_iterables_iterators_2/blob/master/Polygon.py
- Following functions are implemented:
- **__edge__(self)**
    - This is a property.
    - Will give No: of edges(n)
    - This can be set 
- **__radius__(self)**
    - This is a property.
    - Will give circumradius (R)
    - This can be set
- **__repr__(self)**
    - repr function for polygon class. Will give info on No: of edges(n), Circumradius(R).
- **__eq__()**
    - Checks whether a given polygon object is equal or not based on no:of edges and circumradius
- **__gt__**
    - Checks whether a given polygon object is greater than or not based on no:of edges
- **interior_angle(self)**
    - This is a property.
    - Calculates int_angle -> (n−2) * 180 * n.
    - Lazy calculation & stores value. Calculates only if 'n' changes, else provides from stored value.
- **side_length(self)**
    - This is a property.
    - Calculates s = 2 * R * sin(π/n)
    - Lazy calculation & stores value. Calculates only if 'n' or 'R' changes, else provides from stored value.
- **apothem(self)**
    - This is a property.
    - Calculates a = R * cos(π * n)
    - Lazy calculation & stores value. Calculates only if 'n' or 'R' changes, else provides from stored value.
- **area(self)**
    - This is a property.
    - Calculates area = 12 * n * s * a
    - Lazy calculation & stores value. Calculates only if 'n' or 'R' changes, else provides from stored value.    
- **perimeter(self)**
    - This is a property.
    - Calculates perimeter = n * s
    - Lazy calculation & stores value. Calculates only if 'n' or 'R' changes, else provides from stored value.

- File that holds required functions for part 2 (sequence): Polygons.py
- Github Location : https://github.com/anilbhatt1/epai_3_p1_s12_iterables_iterators_2/blob/master/Polygons.py
- Following functions are implemented:
- **__init__(self)**
    - Will store no: of edges in seqeunce (m), common circumradius(R)
- **__repr__(self)**
    - repr function for poly_seq class. Will give info on No: of edges(n) of largest polyon in the sequence and common Circumradius(R).
- **__len__()**
    - Returns length of polygon sequence. This will be m-2 as sides 1 and 2 are not polygons.
- **max_efficiency_polygon(self)**
    - This is a property.
    - This method returns the Polygon with the highest area: perimeter ratio.
    - Lazy calculation. Calculates only if not present in storage. Calculates area:perimeter ratio for each polygon in list, sorts in descending order and returns first element (polygon with highest area:perimeter ratio)
- **__iter__(self)**
    - This is defined to make Polygons an iterable.
    - This calls the class **polyiterator**
- **__polyiterator__(self)**
    - This is a class defined to make Polygons an iterable.
    - **__init__(self, poly_obj)**
        - Essentially accepts the polygon sequence object from which it is called
        - Saves poly_obj in self._poly_obj.
        - Also maintains self._index
    - **__iter__(self)**
        - To maintain this as an iterator. Returns self.
    - **__next__(self)**
        - Returns sides, circumradius and area:perimeter ratio of polygons one by one by creating from **Polygon2** class on the fly  
        - If self._index > self._poly_obj._m raises stopiteration. This avoids indefinite execution.

- Draft Jupyter version where assignment was initially tried out can be found below:
https://github.com/anilbhatt1/epai_3_p1_s12_iterables_iterators_2/blob/master/Iterables_2_Assignment_Draft.ipynb

## Testing
- All the above functions are tested using pytest.
- Testcase file : **test_Polygons.py** (Please note that that 'test_' need to be prefixed for Pytest to automatically identify that it is a testcase file).
- Github Location : https://github.com/anilbhatt1/epai_3_p1_s12_iterables_iterators_2/blob/master/test_Polygons.py
- Test snapshot results as below:
![Test_Pass](https://github.com/anilbhatt1/epai_3_p1_s12_iterables_iterators_2/blob/master/Assignment2_Test_Passed_Snapshot.png)

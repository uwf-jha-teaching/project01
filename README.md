# Geographic Information System (GIS)
[![Points badge](../../blob/badges/.github/badges/points.svg)](../../actions)

## Project Outcomes:
Develop a C++ program that uses:
- Dynamic arrays
- Memory management in classes (rule of three)
- Arrays of objects
- Multiple user-defined classes
- Test case reading

## Preparatory Readings:
- ZyBook primer chapters
- ZyBook chapter 2, 3

## Project overview:
Geographic Information Systems (GIS) are a useful application of technology to
the field of Geography. GIS tools are used in systems such as GCCS, often used
by the military for mission planning and high-level navigation. They are also
used by municipalities for managing resources such as monitoring watersheds for
testing purposes. County tax assessors likewise use such tools for assessing
taxes on property owners.

All of these applications involve efficient and accurate querying of points (for
example a mouse click) to determine whether a query is inside a particular
polygon. The purpose of such queries is often to report the name of the polygon
that contains the query point. The polygons used in GIS systems are often
referred as **parcels**.

Checking whether a point is inside a polygon depends on how the polygon is
stored. For this project, we'll work with convex polygons only, this enables us
to simplify the inclusion check a bit. In our case, polygons will be stored as a
list of vertices given in the clockwise order. Thus, checking if a point is
inside a polygon involves checking whether the point lies **on or to the right**
of all edges if we treat every edge as a directed line following the clockwise
direction.

Given three points, to determine the location of a point **p3** related to the
line from point **p1** to point **p2**, we can use the following formula
`(p2.x - p1.x)(p3.y - p1.y) - (p2.y - p1.y)(p3.x - p1.x)` to calculate the cross
product of two vectors `p2->p1` and `p3->p1`. If this value is negative, **p3**
is on the right to the edge from **p1** to **p2**. If this value is zero, it is
**on the edge**. Both should be consider inside the polygon. You may make a
private boolean function to perform this check.

## Project Requirements:
Your application must function as described below:
1. Your program shall adhere to the test suites provided [here](test/). Read
   the tests and create the required files, classes, and methods. This means
   that all tests must pass in their current configuration.
1. A [makefile](makefile) is provided. Read it to have some understanding of
   the project. Never modify it!.
1. Additionally, you must create a user application that allows a user to
   specify an input file which conforms to the [Sample
   data](#sample-polygonal-data) format given below.
    - Data will be given as alternating `x` and `y` values.
    - Each line of the input file will contain a single polygon.
    - All coordinate values are integer values.
    - The first parcel in the sample data below is a 2x2 square with the bottom
    left vertex at (0,0) and a rectangle that is two units high and six units
    wide with a bottom left vertex at (0,2).
    - Not all inputs will be axis-aligned rectangles, they are just good
    exemplars due to their simplicity.
1. The program must then allow queries to be submitted in the form of **x** and
   **y** coordinates and should report the _title_ of the polygon which contains
   the query point.
    - The user should be prompted for the x coordinate, then prompted for the y
      coordinate as seen in [Sample run](#sample-run) below.

## Sample polygonal data
This sample data is found in [simple-polygons.txt](simple-polygons.txt). A more
complicated input file is in [polygons.txt](polygons.txt), for when you are
ready to test your program against something more complicated.
```
squareParcel 0 0 0 2 2 2 2 0
wideRectangleParcel 0 2 0 4 6 4 6 2
```
## Sample run
```
Please enter the file with the polygon data: bad-file-name.zz
Invalid file name!
Please enter the file with the polygon data: simple-polygons.txt

Coordinates of query point (non-integer quits)
    x: 1
    y: 1
Query point is inside: squareParcel

Coordinates of query point (non-integer quits)
    x: 3
    y: 3
Query point is inside: wideRectangleParcel

Coordinates of query point (non-integer quits)
    x: 7
    y: 7
Query point is inside: Not Found

Coordinates of query point (non-integer quits)
    x: quit

Have a great day!
```

## Implementation Notes:
1. Read the [Test cases](test/) to understand the design of the classes.
1. Read the [autograding configuration](.github/classroom/autograding.json) to
   understand the autograding process.
1. Read the [makefile](makefile) on the targets to run. No need to understand
   the details in this file.
1. Create a project that is object oriented, therefore there should be several
   classes to create.
1. The input files are provided. They match the exact format given above.
1. Your program must compile and pass all tests.
    - This application must be compiled by running `make main` and shall create
    an executable file called `main`.
    - All tests must pass by running together with `make test-all`. You can run
      individual test during development.
    - Automatic tests on memory leak are involved in autograding.
1. To practice the memory management principals learned in class, you must use
   dynamic arrays to store lists of data in your classes. You classes must be
   memory leak free. Memory leakage will be checked and graded in autograding.
1. It is recommended to practice the good coding conventions in your code:
    1. Pass object by reference (make it const as necessary)
    1. Make **const** functions whenever applicable
1. **Particular tricky parts**
    - The ``Point`` class requires an operator overloading on the ``==``
      operator. Do not forget to implement it.
    - The ``void Polygon::parse`` and ``bool GIS::readfile`` methods should
      handle existing data. As they can both work with object with existing
      data in the dynamic array. Clean it up properly before reading in the new
      data.

## Submission Requirements:
1. All code must be added and committed to your local git repository.
2. All code must be pushed to the GitHub repository created when you "accepted"
   the assignment.
    1. After pushing, with `git push origin main`, visit the web URL of your
       repository to verify that your code is there. If you don't see the code
       there, then we can't see it either.
3. Your code must compile and run. The auto-grading tests will indicate your
   score for your submission.
    1. The auto-grading build should begin automatically when you push your code
       to GitHub.
    2. If your program will not compile, the graders will not be responsible for
       trying to test it.
    3. You should get an email regarding the status of your build, if it does
       not pass, keep trying.
4. Do not remove the data files!

## Important Notes:
- Projects will be graded on whether they correctly solve the problem, and
  whether they adhere to good programming practices.
- Projects must be received by the time specified on the due date.
- Please review the academic honesty policy.
    - Note that viewing another student's solution, whether in whole or in part,
      is considered academic dishonesty.
    - Also note that submitting code obtained through the Internet or other
      sources, whether in whole or in part, is considered academic dishonesty.
    - All programs submitted will be reviewed for evidence of academic
      dishonesty, and all violations will be handled accordingly.

## Grading Information:
- Breakdown
    + 80% GitHub Auto-grading
    + 10% Coding style (naming convention, neatness of code, etc)
    + 10% Code organization (modular design, separate files, headers, etc.)
- Auto-grading results can be checked at the top of this document like as a
  badge ***40/80***.
- View details:
    1. On your GitHub repo page, Click the :arrow_forward: **Actions** tab to
       see your graded results.
    1. If it isn't a green check mark (:heavy_check_mark:) then at least part of
       the testing failed.
    1. Click the commit message for the failing version then click "Autograding"
       on the left side of the page.
    1. Follow the :x: path and expand things to see what errors exist.
    1. It is usually **education/autograding@v1** and you can expend this path to
       view the detail.

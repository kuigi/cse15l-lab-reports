## Lab Report 3

# Part 1: Bugs

For this part, I will demonstrate a bug in the `ArrayExamples.java` file using JUnit tests in the `ArrayTests.java` file.
Here, I wrote a JUnit test inputting an array with an even number of elements into the `reverseInPlace()` method, and the buggy program fails the test.
```
@Test
  public void testReverseInPlace2() {
    int[] input1 = {1, 4, 6, 8};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{8, 6, 4, 1}, input1);
  }
```

Here is the resulting output, showing that this test fails. We can see that where we want 4 to be in the reversed array's 3rd element,
we actually get 6, which is the element in the 3rd spot initially.

```
JUnit version 4.13.2
.E..
Time: 0.033
There was 1 failure:
1) testReverseInPlace2(ArrayTests)
arrays first differed at element [2]; expected:<4> but was:<6>        
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)      
        at org.junit.Assert.assertArrayEquals(Assert.java:418)        
        at org.junit.Assert.assertArrayEquals(Assert.java:429)        
        at ArrayTests.testReverseInPlace2(ArrayTests.java:23)
        ... 30 trimmed
Caused by: java.lang.AssertionError: expected:<4> but was:<6>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.java:8)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
        ... 36 more

FAILURES!!!
Tests run: 3,  Failures: 1
```
Here is a JUnit test which ensures that the code does not modify the elements of the array in any way that we don't want it to. It passes as I
make the input 4 elements of the same number.

```
 @Test
  public void testReverseInPlace3() {
    int[] input1 = {4, 4, 4, 4};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{4, 4, 4, 4}, input1);
  }
```

As a result, here is the output of this test (alongside the output of the tests in the starter code, which also pass).

```
Time: 0.035

OK (3 tests)
```
Through these tests (and similar tests that pass in arrays of different sizes), we can see that there is an issue with how `reverseInPlace` deals with 
the second half of the array. Mainly, it's the fact that it *doesn't* deal with it. The second half is not "reversed" to have the first half of the array. 
Instead, it remains the same.  We can change this with the following changes.

Before:
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
AFter:
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i++) {
      int temp = arr[i];
      arr[i] = arr[arr.length - 1 - i];
      arr[arr.length - 1 - i] = temp;
    }
  }
```
In this new version, we ensure that the element we're on in the first half of the array is traded with its counterpart in the second half.
It then replaces the second-half counterpart with the first half, effectively reversing the array of integers.
The bounds of the for-loop are changed to only iterate through half of the array since the first half also does the work for 
the second half.


# Part 2: Researching Commands

In this part, I will be exploring the `grep` command and demonstrating some interesting options and ways to use the command.
We will be using the commands on the `docsearch` folder from Lab 5 as well as the .txt files in it.
All command line options for `grep` and their explanations will be sourced from [this Linux grep help page from geeksforgeeks.org.](https://www.geeksforgeeks.org/grep-command-in-unixlinux/)

This first one will use the usage of the `-n` option with grep.
In one of the files in `technical/biomed`, we can see exactly what line the Results and Conclusion of the report
in this text file.
Inputting:
```
grep -n "Results" technical/biomed/1471-2091-3-23.txt
```
We get:
```
97:        Results
```
This enables us to immediately find where the "Results" section of this article is, which is useful when going over
scientific articles such as this one.
We can do the same for "Conclusion".
Inputting:
```
grep -n "Conclusion" technical/biomed/1471-2091-3-23.txt
```
We get: 
```
452:        Conclusions
```
Again, we can find exactly what line the "Conclusions" section of the article is, which is very useful especially if the article is long and we want to have something to immediately reach a certain section of that article.

A fundamental command for grep is the `-l` command, which searches for files with a certain string in their files.
Example:
```
grep -l "Mitchell" *
```
When you `cd` into `~/docsearch/technical/government/Post_Rate_Comm`, you can see which files which mention Mitchell, producing this output:
```
Mitchell_6-17-Mit.txt
Mitchell_RMVancouver.txt
```
Another example when you `cd` into ~/docsearch/technical/plos`:
```
 grep -l "eukaryotic" *
```
Produces:
```
journal.pbio.0020013.txt
journal.pbio.0020042.txt
journal.pbio.0020133.txt
journal.pbio.0020306.txt
journal.pbio.0020354.txt
journal.pbio.0030076.txt
journal.pbio.0030094.txt
pmed.0020210.txt
```
This presents every file that contains the word "eukaryotic" in its file.

To ensure you get the exact word, and not just words containing that specific substring, you can use the
`-w` option.

For example, when you `cd` into `technical/biomed`, you may want to differentiate when you want the word "tension" versus the word "hypertension".
Here, you can differentiate by using `-w`.
Example:
```
 grep -w  "tension" *
```
Produces:
```
1471-2121-3-4.txt:        stiffness of the cell by introducing tension into the
1471-2121-3-4.txt:        less stiff in surface tension than the wild type parental
1471-2121-3-4.txt:          or surface tension is the 
appropriate parameter to
1471-2156-4-6.txt:          chromatids, and the tension on chromosomes produced by
1471-2202-2-9.txt:          tension applied by the outward migrating growth cone.
1471-2229-2-8.txt:          evaluated by the tension table and pressure plate
1471-2318-3-2.txt:          where there has traditionally been tension between
1471-5945-2-13.txt:        relation to the tension in 
the surrounding ECM, we utilized
1471-5945-2-13.txt:            reduction of tension in the ECM
1471-5945-2-13.txt:          Effect of tension in the 
ECM
1471-5945-2-13.txt:        - We found that matrix tension was dominant over TGFβ1
``` 
And a whole lot of other files!
Compared to doing:
```
 grep -w  "hypertension" *
```
Which produces an entirely different output:

```
1468-6708-3-1.txt:          baseline. Clinical covariates include hypertension,
1468-6708-3-10.txt:        active-controlled hypertension component is designed to
1468-6708-3-10.txt:        the hypertension component 
began in February, 1994, and
1468-6708-3-10.txt:          least 90 mm Hg, or took medication for hypertension, and
1468-6708-3-4.txt:          moderate essential hypertension [ 1 ] . The study
```
And a whole lot of other files!

Finally, here is the option -R for when you want to search for a pattern in a whole lot of files and directories using recursion.
Example (`cd` into `technical/`):
```
$ grep -R "dysregulation" technical/
```
Produces:
```
technical/biomed/1471-2180-2-26.txt:        dysregulation of cyclin D
technical/biomed/1471-2202-2-16.txt:        dysregulation of PLD2 activity in AD. The first is based on     
technical/biomed/1471-2202-2-16.txt:        dysregulation of PC metabolism. Indeed evidence of an
technical/biomed/1471-2210-1-10.txt:        test if a 
dysregulation of MAP kinases was associated with      
technical/biomed/1471-2210-1-10.txt:        It has been suggested that a dysregulation of MAP
technical/biomed/1471-230X-3-3.txt:        IBD [ 48 49 50 ] . Moreover, dysregulation of cytokine
technical/biomed/1471-2377-2-4.txt:        nitric oxide pathway dysregulation [ 5 9 ] suggesting
technical/biomed/1471-244X-2-9.txt:        dysregulation of body weight. The role of impulsivity in
technical/biomed/1477-7827-1-9.txt:        associated 
with dysregulation of folliculogenesis and
technical/biomed/ar612.txt:        osteoclast dysregulation leads to osteoporosis (decreased
technical/biomed/ar774.txt:        unknown. Immune dysregulation appears to play a key
technical/plos/pmed.0020162.txt:        ultimately harmful dysregulationâ€”of physiological systems that respond
technical/plos/pmed.0020273.txt:        were ubiquitously altered in both IBD and non-IBD samples, reflecting dysregulation of
```
Which shows the appearance of dysregulation in both the `biomed/` and `plos/` directory files in the overall directory `technical/`.
You can use this on another search term which you might think may show up in multiple disciplines, such as those covered in the text files in this folder. 
Example, the city Philadelphia:
```
grep -R "Philadelphia" technical/
```
Produces:
```
technical/911report/chapter-13.3.txt:                Philadelphia Inquirer, Aug. 21, 1998, p. A1. For a reaction to the later criticism
technical/911report/chapter-7.txt:                flew from Fort Lauderdale to Philadelphia, where he trained at Hortman Aviation and
technical/biomed/1471-2121-3-18.txt:          Center, 
Philadelphia, PA, [ 47 ] ). The pEBG-JNK was a        
technical/biomed/1471-2172-3-4.txt:          Bergelson, (Children's Hospital of Philadelphia,
technical/biomed/1471-2172-3-4.txt:          Philadelphia, PA). The forward primer,
technical/biomed/1471-2172-3-9.txt:          cytokine 
was a kind gift from Trinchieri G, Philadelphia,      
technical/biomed/1471-2202-2-9.txt:          Neurology, Children's Hospital, Philadelphia, PA) were
technical/biomed/1471-2202-3-19.txt:          Laboratories (Philadelphia, PA), Win 444,441 was obtained     
technical/biomed/1471-2210-3-1.txt:          (Philadelphia, PA), Win 444,441 was from Sterling
technical/biomed/1471-2334-2-27.txt:          Philadelphia, PA. Cellulose acetate phthalate (CAP) was a     
technical/biomed/1471-2415-3-1.txt:          Interchange (Philadelphia, PA). Lenses were enucleated
technical/biomed/1471-2490-3-2.txt:        Medical Center, Philadelphia, Marcella et al [ 8 ] noted an      
```
Among many other files (omitted for sanity)!

As you can see, you can specify what you want `grep` to do and tailor it specifically to your use cases, and it is important
to know what each option does and what each option can't do in order to get exactly what you want.


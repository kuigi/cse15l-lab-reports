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

In this part, I will be exploring the `find` command and demonstrating some interesting options and ways to use the command.


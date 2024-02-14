# **Lab Report 3 -- Zhenhan Hu(A17282448)**
---
# **Part 1 - Bugs**
## *`static int[] reversed` method in `ArrayExamples` class in `ArrayExamples.java`*
**The original buggy program:**
```
public class ArrayExamples {
  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
}
```
We should employ JUnit test cases in `ArrayTests.java` to verify the functionality of the method. Throughout the debugging process shown below, several JUnit tests were designed and executed, revealing through their symptoms (terminal outputs and error messages I saw) that the initial program exhibited failures in several cases, yet succeeded in others. 

## *An input that doesn't induce a failure as a JUnit test*
```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
  @Test
  public void testReversedEmpty() {
    int[] emptyArray = { };
    int[] reversedemptyArray = ArrayExamples.reversed(emptyArray);
    assertArrayEquals(new int[]{ }, reversedemptyArray);
  }
}
```
[image: no_failure_inducing_test]

## *A failure-inducing input as a JUnit test*
```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
  @Test
  public void testReversedEmpty() {
    int[] emptyArray = { };
    int[] reversedemptyArray = ArrayExamples.reversed(emptyArray);
    assertArrayEquals(new int[]{ }, reversedemptyArray);
  }

  @Test
  public void testReversedNonEmpty() {
    int[] nonEmptyArray = {1, 2, 3};
    int[] reversedemptyArray = ArrayExamples.reversed(nonEmptyArray);
    assertArrayEquals(new int[]{3, 2, 1}, reversedemptyArray);
  }
}
```
[image: failure_inducing_test_output]
[image: failure_inducing_test]
Explanation: The `reversed` method failed nonempty input array `{1, 2, 3}` because, in the `for` loop, original array at index i, `arr[i]`, is being assigned the value of `newArray[arr.length - i - 1]`, but `newArray` with the same capacity is created initially empty, which simply gives 0 instead of intended number. It passed empty input array since input array is empty and the loop inside the reversed method will not execute, thus no incorrect swapping or assignments are made, and the method will simply return a new empty array. Thus, inside the `for` loop, it should be the other way around: newArray should be filled with the values from arr in reversed order, `newArray[i] = arr[arr.length - i - 1];`. However, there is still an issue with the nonempty input array, but this time, different error message (symptom) was given, realizing the return array is not reversed compare to the input...<br>
[image: new_failure_inducing_test_output]
[image: new_failure_inducing_test]
<br>
Explanation: It should return a **new array** with the elements of the input array in reversed order, however, the current implementation modifies the input array `arr` in place and returns it, rather than returning a new reversed array. After fixing it, everything works as intended. (Note: More test cases added)
```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
  @Test
  public void testReversedEmpty() {
    int[] emptyArray = { };
    int[] reversedemptyArray = ArrayExamples.reversed(emptyArray);
    assertArrayEquals(new int[]{ }, reversedemptyArray);
  }

  @Test
  public void testReversedNonEmpty1() {
    int[] nonEmptyArray = {1, 2, 3};
    int[] reversedemptyArray = ArrayExamples.reversed(nonEmptyArray);
    assertArrayEquals(new int[]{3, 2, 1}, reversedemptyArray);
  }

  @Test
  public void testReversedNonEmpty2() {
    int[] nonEmptyArray = {4, 2, 3, 4};
    int[] reversedemptyArray = ArrayExamples.reversed(nonEmptyArray);
    assertArrayEquals(new int[]{4, 3, 2, 4}, reversedemptyArray);
  }

  @Test
  public void testReversedNonEmpty3() {
    int[] nonEmptyArray = {5};
    int[] reversedemptyArray = ArrayExamples.reversed(nonEmptyArray);
    assertArrayEquals(new int[]{5}, reversedemptyArray);
  }
}
```
[image: successful_junit]


## *The before-and-after code change required to fix it*
[image: before&after]
**Issues Summary**:
The method is attempting to gives a new array from input array in reversed order, but it contains several issues. Specifically, inside the `for` loop, `arr[i]` is being assigned the value of `newArray[arr.length - i - 1]`, but `newArray` is empty. It should be the other way around: `newArray` should be filled with the values from `arr` in reversed order. After that, it should return the new array with the elements of the input array in reversed order. However, the current implementation modifies the input array arr in place and returns it, rather than returning a new reversed array.
---
# **Part 2 - Researching Commands**

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
We should employ JUnit test cases to verify the functionality of the method. Throughout the debugging process shown below, several JUnit tests were designed and executed, revealing through their symptoms (terminal outputs and error messages I saw) that the initial program exhibited failures in several cases, yet succeeded in others. 

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
![Image](/images/report3-images/no_failure_inducing_test.png)

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
![Image](/images/report3-images/failure_inducing_test_output.png)
![Image](/images/report3-images/failure_inducing_test.png)
Explanation: The `reversed` method failed nonempty input array `{1, 2, 3}` because, in the `for` loop of the method, original input array at index i, `arr[i]`, is being assigned the value of `newArray[arr.length - i - 1]`, but `newArray` with the same capacity is created initially empty, which simply gives 0 instead of intended number. It did not induce a failure for empty input array since input array is empty and the loop inside the reversed method will not execute, thus no incorrect swapping or assignments are made, and the method will simply return the empty array. Thus, inside the `for` loop, it should be the other way around: `newArray` should be filled with the values from `arr` in reversed order, `newArray[i] = arr[arr.length - i - 1];`. <br>
However, there is still an issue with the nonempty input array, but this time, different error message (symptom) was given, realizing the returned array is not reversed compare to the input array...<br>
![Image](/images/report3-images/new_failure_inducing_test_output.png)
![Image](/images/report3-images/new_failure_inducing_test.png)
<br>
Explanation: It should return a **new array** with the elements of the input array in reversed order, however, after assign elements in the new array `newArray` with elements from input array `arr` in reversed order, the current implementation returns unchanged `arr` rather than returning a new reversed array. After fixing it, everything works as intended. (Note: More test cases added)
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
![Image](/images/report3-images/successful_junit.png)

## *The before-and-after code change required to fix it*
**Before**
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
**After**
```
public class ArrayExamples {
  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }
}
```
![Image](/images/report3-images/before&after.png)

Issues Summary: The method is attempting to gives a new array from input array in reversed order, but it contains several issues. Specifically, inside the `for` loop, `arr[i]` is being assigned the value of `newArray[arr.length - i - 1]`, but `newArray` is empty. It should be the other way around: `newArray` should be filled with the values from `arr` in reversed order. After that, it should return the new array with the elements of the input array in reversed order. However, the current implementation modifies the input array arr in place and returns it, rather than returning a new reversed array.

---
# **Part 2 - Researching Commands**
Citation: I consulted geeksforgeeks.org for more grep command-line options such as `-i` and `-v` and their examples, then I tried my own in `docsearch` workspace. https://www.geeksforgeeks.org/grep-command-in-unixlinux/
## *4 interesting command-line options of 'grep'*
**`grep -r`**
The command-line option of `-r` tells `grep` to read all the files under each directory recursively. This makes the search range covers across multiple files and directories. As you can see, `grep -r "United Nations"` searches "United Nations" on files under multiple directories including `./technical/plos`, `./technical/911report`, and `./technical/government/`. The matched results of `grep -r "Anthem"` covers several different directories and files as well.
![Image](/images/report3-images/grep-r1.png)
![Image](/images/report3-images/grep-r2.png)

**`grep -l`**
The command-line option of `-l` tells `grep` to list the names of files with matching lines. The filenames are displayed only, not the matched lines. In the two examples below, `grep -l` gives the files names of matched results for "UAE" under all .txt files within `./technical/911report` directory, and for "North America" under all .txt files within `./technical/plos`.
![Image](/images/report3-images/grep-l1.png)
![Image](/images/report3-images/grep-l2.png)

**`grep -i`**
The command-line option of `-i` tells `grep` to be case insensitive for matching. In the two examples below, result that matched "in clinical trials" is also included for the searching key "in CLINICAL trials", and "scientific contributions" is included for "SCIENTIFIC contributions".
![Image](/images/report3-images/grep-i1.png)
![Image](/images/report3-images/grep-i2.png)

**`grep -v`**
The command-line option of `-v` tells `grep` to giving matching lines inverted, which means it only shows the lines that do not match the given pattern. In the two examples below, `grep -v` gives lines that does not match the given argument (case-sensitive) for "whistleblow" within `./technical/plos/pmed.0020281.txt`, and for "primate" within `./technical/plos/pmed.0020278.txt`.
![Image](/images/report3-images/grep-v1.png)
![Image](/images/report3-images/grep-v2.png)

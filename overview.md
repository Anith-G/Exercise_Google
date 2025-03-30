# API Reference: findNeedles Method

# Overview
The findNeedles method searches for occurrences of specified words ("needles") in a given text ("haystack") and prints the count for each needle found.

# Method Signature
``` shell
public static void findNeedles(String haystack, String[] needles)
```

# Parameters
* haystack (String): The input text in which to search for specified words.
* needles (String[]): An array of words to search for in the haystack. The length of this array must not exceed 5.

# Behavior
1. If the needles array contains more than 5 words, the method prints an error message ("Too many words!") and does not proceed further.

1. The method tokenizes the haystack by splitting it based on whitespace and common delimiters (" ' \t\n\b\f\r").

1. It counts occurrences of each needle and stores them in an integer array (countArray).

1. Finally, it prints the count of each needle.


# Example Usage

## Example 1: Valid Input

``` Shell
public class Main {
    public static void main(String[] args) {
        String text = "The quick brown fox jumps over the lazy dog. The fox is clever.";
        String[] words = {"fox", "dog", "cat"};
        findNeedles(text, words);
    }
}
```
## Output:

``` Shell
fox: 2
dog: 1
cat: 0
```
## Example 2: Invalid Input (Exceeding the Word Limit)
``` Shell
String text = "The quick brown fox jumps over the lazy dog.";
String[] words = {"quick", "brown", "fox", "jumps", "lazy", "dog"};
findNeedles(text, words);
```
## Output
``` Shell
Too many words!
```

# Code Improvement Suggestions
1. Optimize Memory Usage: Instead of splitting haystack into an array (words), consider using a Scanner or StringTokenizer to process words one at a time. This prevents creating a potentially large array, reducing memory overhead.
2. Improve Performance: Use a HashMap<String, Integer> to store word frequencies while iterating over haystack. Then, simply look up each needle in the map, reducing redundant computations.
3. Enhance Readability and Maintainability:
   * 	Use equals instead of compareTo for string comparison.
   * 	Replace System.err.println with proper exception handling (IllegalArgumentException).
   * 	Utilize enhanced for-loops to improve readability.

  # Benefits of the Enhanced Version
  * Lower Memory Usage: No unnecessary array storage for split words.
  * Faster Execution: Single-pass processing of haystack.
  * Better Readability: More structured and maintainable code.

# Suggested Code Enhancement

```Shell
import java.util.HashMap;
import java.util.Map;

public static void findNeedles(String haystack, String[] needles) {
    if (needles.length > 5) {
        throw new IllegalArgumentException("Too many words!");
    }

    // Use a HashMap to count word occurrences
    Map<String, Integer> wordCount = new HashMap<>();
    for (String word : haystack.split("\\W+")) {  // Split using non-word characters
        wordCount.put(word, wordCount.getOrDefault(word, 0) + 1);
    }

    // Print occurrences for each needle
    for (String needle : needles) {
        System.out.println(needle + ": " + wordCount.getOrDefault(needle, 0));
    }
}
```

# API Document Template

API documentation for the **_`findNeedles`_** method.

## Find Needles in a Haystack

The **_`findNeedles`_** method counts the number of occurrances of up to five specific words (*needles*) within a given text (*haystack*).

Here is a sample with a Java code snippet, followed by details of its parameters and the possible outputs:

**METHOD:** *`findNeedles`*
```java
public static void findNeedles(String haystack, String[] needles) {
  if (needles.length > 5) {
    System.err.println("Too many words!");
  } else {
    int[] countArray = new int[needles.length];
    for (int i = 0; i < needles.length; i++) {
      String[] words = haystack.split("[ \"\'\t\n\b\f\r]", 0);
      for (int j = 0; j < words.length; j++) {
        if (words[j].compareTo(needles[i]) == 0) {
        countArray[i]++;
        }
      }
    }
    for (int j = 0; j < needles.length; j++) {
    System.out.println(needles[j] + ": " + countArray[j]);
    }
  }
}
```

|PARAMETER|DESCRIPTION|TYPE|REQUIRED|
|---|---|---|---|
|`haystack`|Text to be inspected.|string|yes|
|`needles`|Words to be searched within the given text.|string|yes|

<br/>**POSSIBLE OUTPUTS:**

* For **up to 5** needles searched, the output displays the number of ocurrances of each needle:
<br/>`[needle_value]: [total_ocurrances]`

* If **more than 5** needles are searched, the output displays an error with the following message:
<br/>`"Too many words!"`


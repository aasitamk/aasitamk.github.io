# API Document Template

[This page](aasitamk.github.io/TESTE.html) contains the API documentation for the `findNeedles` method.

## Overview

The `findNeedles` method counts the number of occurrances of up to five specific words within a given text.
<br/> Here is a Java sample, followed by the description of its query parameters:

<aside class="request"><span class="method">METHOD</span> <span class="endpoint">findNeedles</span></aside>

```
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

|Parameter|Description|Type|Mandatory?|
|---|---|---|---|
|haystack|Text to be searched in.|string|yes|
|needles|Words to be searched within the given text.|string|yes|

## Responses

**5 words or less = successful operation**
{needle}: {number}

**more than 5 words = error message**
"Too many words!"

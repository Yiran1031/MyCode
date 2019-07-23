### Basic Operation
---
#### String

#### 1. split a String by symbol 

**approach**

- variable
  - ArrayList
  - StringBuilder
- Iterator the String object s by index i;
- If s.charAt(i)  !=  0, add it to StringBuilder object
- If s.charAt(i) ==  ' ',add StringBuilder Object to Arraylist if needed 

```java
   // split a String by " "
   public String[] split(String s)
    {
        List<String> words = new ArrayList<String>();
        StringBuilder word = new StringBuilder();
        for(int i = 0; i < s.length(); i++)
        {
          // if there is exist a space and the length of word != 0 add it to ArrayList
          // create a new StringBuilder
            if(s.charAt(i) == ' ')
            {
                if(word.length() != 0)
                    words.add(word.toString());
                word = new StringBuilder();
            }else
            {
              // append the new character to StringBuilder
                word.append(s.charAt(i));
            }
        }
     //add last word and return.
     if(word.length() != 0)
        words.add(word.toString());
        return words.toArray(new String[words.size()]);
    }
```
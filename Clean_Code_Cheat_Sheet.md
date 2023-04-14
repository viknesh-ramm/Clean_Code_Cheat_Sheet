# Clean Code Cheat Sheet

## Variables

### 1. Use Intention Revealing Names

Wrong ❌

```c#
 int x; // elapsed time in milliseconds
```

Correct  ✅

```c#
 int elapsedTimeInMilliSeconds;
```

### 2. Use Pronouncable Names

Wrong ❌

```c#
 string hhmmss;
```

Correct  ✅

```c#
 string timeStamp;
```

### 3. Use Searchable Names

Wrong ❌

```c#
  int e;
  string an;
  float t;
```

Correct  ✅

```c#
 int elapsedSeconds;
 string authorName;
 float total;
```

Though the IDEs of today have the ability to get the references of
variables, it is highly recommended to **NOT** use single character variable
names.

### 4. Avoid Disinformation

Wrong ❌

```c#
  string accountNamesList;
```

Correct  ✅

```c#
 string commaSeparatedAccountNames; 
```

Do not refer to a grouping of entites as a List unless it's actually a List. The word List means something specific to programmers.

### 5. Avoid Noise Words

Wrong ❌

```c#
  string nameString;
```

Correct  ✅

```c#
 string name; 
```

### 6. Avoid Inconsistent Spelling

Wrong ❌

```c#
  string colorCode;
  string selectedColour;

```

Correct  ✅

```c#
  string colorCode;
  string selectedColor;
```

## Functions

### 1. Function names should be a verb or verb phrase

Wrong ❌

```c#
  public string StudentName()
  {
    ...
    return studentName;
  }
```

Correct  ✅

```c#
  public string GetStudentName()
  {
    ...
    return studentName;
  }
```

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

### 2. Functions Should be Small

It is highly recommended to have a maximum of **20 lines** of code within a single function

Bigger functions have to be broken down to multiple smaller functions.

### 3. Lines within blocks should be in single line​

Wrong ❌

```c#
if (((age > 21 && age < 45) && gender == "female" ) || ((age > 18 && age < 50) && gender == "male"))
{
  ...
}​
```

Correct  ✅

```c#
bool isAgedFemale = (age > 21 && age < 45) && gender == "female";​
bool isAgedMale = (age > 18 && age < 50) && gender == "male";
if (isAgedMale || isAgedFemale)​
{
  ...
}​
```

### 4. Avoid Nested Structures

Wrong ❌

```c#
if ()
{
  if()
  {
    if()
    {

    }
  }
}
​
```

Correct  ✅

```c#
if ()
{
  functionCall1()
}​
else
{
  functionCall2()
}
```

1. Do one thing – Only one level below the abstraction​
2. Check if one more function can be extracted​

### 5. Functions can have 0,1 or maximum 2 arguments only

Having more than 2 arguments might

1. Makes testing harder for all combinations
2. Make remembering order harder

> **Note**
> If there is a need to pass more than 2 arguments, it is recommended to encapsulate the values as a Class object and pass it to the function

### 6. A function should do only one thing

Wrong ❌

```c#
bool IsPasswordValid(string userName, string password)
{
  string encodedPasswordInDatabase = GetPasswordFromDatabase(userName);

  if (encodedPasswordInDatabase != null)
  {
    string encodedGivenPassword = Encoder.EncodePassword(password)
    if (encodedGivenPassword == encodedPasswordInDatabase)
    {
      CreateSessionInformation(userName);
      return true;
    }
  }
  return false;
}
​
```

Correct  ✅

```c#
bool IsPasswordValid(string userName, string password)
{
  string encodedPasswordInDatabase = GetPasswordFromDatabase(userName);

  if (encodedPasswordInDatabase != null)
  {
    string encodedGivenPassword = Encoder.EncodePassword(password)
    if (encodedGivenPassword == encodedPasswordInDatabase)
    {
      return true;
    }
  }
  return false;
}

// Create session information outside the IsPasswordValid function. The function should do only password validation

if (IsPasswordValid(userName, password))
{
  CreateSessionInformation(userName);
}
```

### 7. Function should either do something or answer something, not both

Wrong ❌

```c#
bool setAttribute(string attributeName, string value)
{
  if (attributes.exists(attributeName))
  {
      attributes[attributeName] = value;
      return true;
  }
  return false;
}​
```

Correct  ✅

```c#
void setAttribute(string attributeName, string value)
{
  attributes[attributeName] = value;
}

bool isAttributeAvailable(string attributeName)
{
  return attributes.exists(attributeName);
}

if (isAttributeAvailable(attributeName))
{
  setAttribute(attributeName, value)
}
```

### 8. Use one word per concept

Wrong ❌

```c#
string GetStudentName(int id)
{
  ...
}

Student FetchStudent(int id)
{
 ...
}

Student[] RetrieveAllStudents()
{
  ...
}
```

Correct  ✅

```c#
string GetStudentName(int id)
{
  ...
}

Student GetStudent(int id)
{
 ...
}

Student[] GetAllStudents()
{
  ...
}
```

## Comments

### Explain yourself in code

Wrong ❌

```c#
// Check to see if the employee is eligible for full benefits
if ((employee.flags & HOURLY_FLAG) && (employee.age > 65))
```

Correct  ✅

```c#
if (employee.isEligibleForFullBenefits())
```

### Good Comments ✅

#### 1. Legal Comments

Copyright information or licensing information might be added to the code

#### 2. Informative Comments

```c#
// format matched kk:mm:ss EEE, MMM dd, yyyy
public string  pattern = "\\d*:\\d*:\\d* \\w*, \\w* \\d*, \\d*";
```

#### 3. Explanation of Intent

```c#
// Creating a large number of threads to achieve race condition
for (int i = 0; i < 25000; i++) {
  Thread thread = new Thread(widgetBuilderThread);
  thread.start();
}
```

#### 4. Clarification

```c#
assertTrue(a.compareTo(a) == 0); // a == a
```

Sometimes clarification is risky as there is a possibility of having it wrong. So
please be careful.

#### 5. Warning of Consequences

```c#
public static SimpleDateFormat makeStandardHttpDateFormat()
{
  //SimpleDateFormat is not thread safe, 
  //so we need to create each instance independently.
  SimpleDateFormat df = new SimpleDateFormat("EEE, dd MMM yyyy HH:mm:ss z");
  df.setTimeZone(TimeZone.getTimeZone("GMT"));
  return df;
}
```

#### 6. TODO Comments

```c#
//TODO: these are not needed
// We expect this to go away when we do the checkout model
protected VersionInfo makeVersion() 
{
  return null;
}
```
When adding a to-do comment, it is always a good practice to include the link of the story/feature/task which would be used to track that work.

### Bad Comments ❌

#### 1. Mumbling

```c#
public void LoadProperties()
{
  try
  {
    File.ReadAllText("./properties.config")
  }
  catch (IOException exception)
  {
    // if the file doesn't exist load the defaults
  }
}
```

Here the comment says when the file is not present, load the default. But who loads the defaults and what are the defaults are not mentioned clearly.

#### 2. Redundant Comments

```c#
// This is a utility function that closes the file when the pointer is not null
private void CloseFile(File filePointer)
{  
  if (filePointer != null)
  {
    filePointer.Close()
  }
}
```

Avoid writing comments when we can understand easily from the code.

#### 3. Noise Comments

```c#
class Student
{
  // Name of the student
  public string Name { get; set; }

  // Default Constructor
  public Student()
  {
  }
}

```

Do not restate the obviou.s

#### 4. Closing Brace Comments

```c#
public class Program
{
    public static void main(String[] args)
    {
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        string line;
        int lineCount = 0;
        int charCount = 0;
        int wordCount = 0;
        try
        {
            while ((line = in.readLine()) != null)
            {
              lineCount++;
              charCount += line.length();
              String words[] = line.split("\\W");
              wordCount += words.length;
            } //while
            Console.WriteLine("wordCount = " + wordCount);
            Console.WriteLine("lineCount = " + lineCount);
            Console.WriteLine("charCount = " + charCount);
            } // try
            catch (IOException e) {
              System.err.println("Error:" + e.getMessage());
            } //catch
    } //main
}
```

Do not clutter the code with closing braces comments.

#### 5. Commented out code

```c#
  InputStreamResponse response = new InputStreamResponse();
  response.setBody(formatter.getResultStream(), formatter.getByteCount());
  // InputStream resultsStream = formatter.getResultStream();
  // StreamReader reader = new StreamReader(resultsStream);
  // response.setContent(reader.read(formatter.getByteCount()));
```

**DO NOT** leave the commented out code in the repo. It creates a lot of confusion and clutters the code.
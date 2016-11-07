# CleanCode

## Chapter 4 : Comment

> "Comment are always failure"

### Comment Do Not Make Up for The Bad Code
> "Ooh, I'd better commnt that!" "No! You'd better clean it"
  
### Explain Yourself in Code
```java
// Check to see if the employee is eligible for full benefits
if ((employee.flags & HOURLY_FLAG) &&
(employee.age > 65))
```
  
- Or this?
```java
if (employee.isEligibleForFullBenefits())
```

### Good Comments
####Legal Comments
```swift
//  Copyright © 2016 Space EDSA. All rights reserved.
```

#### Informative Comments
```swift
// format matched kk:mm:ss EEE, MMM dd, yyyy
Pattern timeMatcher = Pattern.compile(
 "\\d*:\\d*:\\d* \\w*, \\w* \\d*, \\d*");
```

####Explanation of Intent
```java
public void testConcurrentAddWidgets() throws Exception {

	WidgetBuilder widgetBuilder =
		new WidgetBuilder(new Class[]{BoldWidget.class});
	String text = "'''bold text'''";
	ParentWidget parent =
		new BoldWidget(new MockWidgetRoot(), "'''bold text'''");
	AtomicBoolean failFlag = new AtomicBoolean();
	failFlag.set(false);
	
	//This is our best attempt to get a race condition
	//by creating large number of threads.
	for (int i = 0; i < 25000; i++) {
		WidgetBuilderThread widgetBuilderThread =
		new WidgetBuilderThread(widgetBuilder, text, parent, failFlag);
		Thread thread = new Thread(widgetBuilderThread);
		thread.start();
	}
	
	assertEquals(false, failFlag.get());
}
```
 
####Clarification
```swift
public void testCompareTo() throws Exception
{
WikiPagePath a = PathParser.parse("PageA");
WikiPagePath ab = PathParser.parse("PageA.PageB");
WikiPagePath b = PathParser.parse("PageB");
WikiPagePath aa = PathParser.parse("PageA.PageA");
WikiPagePath bb = PathParser.parse("PageB.PageB");
WikiPagePath ba = PathParser.parse("PageB.PageA");

assertTrue(a.compareTo(a) == 0); // a == a
assertTrue(a.compareTo(b) != 0); // a != b
assertTrue(ab.compareTo(ab) == 0); // ab == ab
assertTrue(a.compareTo(b) == -1); // a < b
assertTrue(aa.compareTo(ab) == -1); // aa < ab
assertTrue(ba.compareTo(bb) == -1); // ba < bb
assertTrue(b.compareTo(a) == 1); // b > a
assertTrue(ab.compareTo(aa) == 1); // ab > aa
```

####Warning of Consequences
```swift
// Don't run unless you
// have some time to kill.
public void _testWithReallyBigFile()
{
writeLinesToFile(10000000);
response.setBody(testFile);
response.readyToSend(this);
String responseString = output.toString();
assertSubString("Content-Length: 1000000000", responseString);
```

####TODO Comments
```swift
//TODO-MdM these are not needed
// We expect this to go away when we do the checkout model
protected VersionInfo makeVersion() throws Exception
{
return null;
}
```

####Amplification
```swift
String listItemContent = match.group(3).trim();
// the trim is real important. It removes the starting
// spaces that could cause the item to be recognized
// as another list.
new ListItemWidget(this, listItemContent, this.level + 1);
return buildList(text.substring(match.end()));
```

###Bad Comments
####Mumbling
```swift
public void loadProperties()
{
  try
  {
    String propertiesPath = propertiesLocation + "/" + PROPERTIES_FILE;
    FileInputStream propertiesStream = new FileInputStream(propertiesPath);
    loadedProperties.load(propertiesStream);
  }
  catch(IOException e)
  {
    // No properties files means all defaults are loaded
  }
}
```

####Redundant Comments
```java
// Utility method that returns when this.closed is true. Throws an exception
// if the timeout is reached.
public synchronized void waitForClose(final long timeoutMillis)
  throws Exception
  {
    if(!closed)
      {
        wait(timeoutMillis);
        if(!closed)
          throw new Exception("MockResponseSender could not be closed");
      }
  }
```
####Misleading Comments

####Mandated Comments
```java
 /**
 *
 * @param title The title of the CD
 * @param author The author of the CD
 * @param tracks The number of tracks on the CD
 * @param durationInMinutes The duration of the CD in minutes
 */
 public void addCD(String title, String author,
 int tracks, int durationInMinutes) {
 CD cd = new CD();
 cd.title = title;
 cd.author = author;
 cd.tracks = tracks;
 cd.duration = duration;
 cdList.add(cd);
 }
 ```
 
####Journal Comments
 ```java
 * Changes (from 11-Oct-2001)
 * --------------------------
 * 11-Oct-2001 : Re-organised the class and moved it to new package
 * com.jrefinery.date (DG);
 * 05-Nov-2001 : Added a getDescription() method, and eliminated NotableDate
 * class (DG);
 * 12-Nov-2001 : IBD requires setDescription() method, now that NotableDate
 * class is gone (DG); Changed getPreviousDayOfWeek(),
 * getFollowingDayOf
 ```
 
####Noise Comments
```java
/**
* Returns the day of the month.
*
* @return the day of the month.
*/
public int getDayOfMonth() {
return dayOfMonth;
```

```java
/** The name. */
private String name;
/** The version. */
private String version;
```

####Commented-Out Code
```java
InputStreamResponse response = new InputStreamResponse();
response.setBody(formatter.getResultStream(), formatter.getByteCount());
// InputStream resultsStream = formatter.getResultStream();
// StreamReader reader = new StreamReader(resultsStream);
// response.setContent(reader.read(formatter.getByteCount()));
```

####Too Much Information
####Inobvious Connection

# Lab Report 5

## Part 1: Debugging Scenario

A student makes an Edstem post as follows:

**Anonymous:**
Someone help me pLEASEE!!!!!!!!!! I'm trying to test out my chat server, but I keep on failing this test that I swear
should pass even though it's failing. It keeps on giving me this error whenever I run the test, but I know my code for the server
is right and I tested it using the URL just now.

Here's the output for the tester:

![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/a6f1c14f-b2a9-4efb-92d0-6062504222e0)

I'm not sure what's wrong, everything looks the same as the other tests and I think I'm following the
right syntax when I look at my code but it's still saying I have invalid parameters, can I get some help on where to look to fix this? Thanks.

**AwesomeTA:**

Hi, 

It looks like your test case is failing because according to your program, the URL that you are passing in actually has invalid parameters. This could be for a variety of reasons, but it's hard to debug this without knowing what your code looks like. For starters, try and see if the URLs you use in your failed test prints the same result when accessing it via `curl` or your web browser, and that it is the same syntax as your passed tests. It could be that there is some incorrect usage of your methods when you pass in your URL, leading to an "Invalid parameters" mesasge. If it does, look closely and see if the URL matches the keywords you use in your program to indicate user and message.

Hope this helps!

**Anonymous:**
Hi, I used the URLs that I put in that specific failed test in my web browser after running the server files, and this was the output:
![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/5dee6fdf-f876-428a-964d-cab00fa4456c)

![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/5aa093ff-f62b-4944-b33d-a145d48dddc5)

Compared to one of the URLs from my passing tests:

![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/020d9562-184a-4927-82e4-3b42b31c84d1)

Upon further inspection, it seems like there was an error in my parameters for both of the URLs I had for my failing test. The parameter `name` should have been the word `user` instead, and since I was using `name` instead of `user` both of the URLs I used weren't working. I first tested this using my web browser as so, which yielded the text I want:
![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/dea68f92-74e3-4e4c-9dd6-637265884395)
![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/26d098da-785b-4532-9db3-254fb738daf3)

In my test, I fixed the URLs I passed into the test by changing the `name` parameters to `user`, and the tests passed as such:

![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/e180258a-026b-4779-9df9-a46b5f9ecfaf)

Thanks for the help!


## Post Debug Debrief

During this debugging scenario, here was the file and directory structure that the student used.
```
chat-server/
  chathistory/
    chathistory1.txt
    chathistory2.txt
    chathistory3.txt
  lib/
    hamcrest-core-1.3.jar
    junit-4.13.2.jar
  .gitignore
  ChatHistoryReader.java
  ChatServer.java
  Handlertests.java
  Server.java
  test.sh
  run.sh
```
The bug was encountered when the following lines were executed in the command terminal (using a testing script that contains the compilation and run commands for the relevant files):
```
$ bash test.sh
JUnit version 4.13.2
...E
Time: 0.051
There was 1 failure:
1) handleRequestMulti(HandlerTests)
org.junit.ComparisonFailure: expected:<[onat: good luck

edwin: with your demo!

]> but was:<[Invalid parameters: name=edwin&message=with your demo!]>
        at org.junit.Assert.assertEquals(Assert.java:117)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at HandlerTests.handleRequestMulti(HandlerTests.java:34)

FAILURES!!!
Tests run: 3,  Failures: 1
```
The erroneous test file started as this:
```
import static org.junit.Assert.*;
import org.junit.*;
import java.net.URI;

public class HandlerTests {
  @Test
  public void handleRequest1() throws Exception {
    ChatHandler h = new ChatHandler();
    String url = "http://localhost:4000/chat?user=joe&message=hi";
    URI input = new URI(url);
    String expected = "joe: hi\n\n";
    assertEquals(expected, h.handleRequest(input));
  }

  @Test
  public void handleRequest2() throws Exception {
    ChatHandler h = new ChatHandler();
    // NOTE: %20 is the way to put a space in the parameters of a URL
    String url = "http://localhost:4000/chat?user=edwin&message=happy%20friday!";
    URI input = new URI(url);
    String expected = "edwin: happy friday!\n\n";
    assertEquals(expected, h.handleRequest(input));
  }

  @Test
  public void handleRequestMulti() throws Exception {
    ChatHandler h = new ChatHandler();
    String url1 = "http://localhost:4000/chat?name=onat&message=good%20luck";
    String url2 = "http://localhost:4000/chat?name=edwin&message=with%20your%20demo!";
    URI input1 = new URI(url1);
    URI input2 = new URI(url2);
    String expected = "onat: good luck\n\nedwin: with your demo!\n\n";
    h.handleRequest(input1);
    assertEquals(expected, h.handleRequest(input2));
  }
}
```

This is the `ChatServer.java` file that the student used for their implementation of the server:

```
import java.io.IOException;
import java.net.URI;
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileWriter;

class ChatHandler implements URLHandler {
  String chatHistory = "";

  public String handleRequest(URI url) {

    // expect /chat?user=<name>&message=<string>
    if (url.getPath().equals("/chat")) {
      String[] params = url.getQuery().split("&");
      String[] shouldBeUser = params[0].split("=");
      String[] shouldBeMessage = params[1].split("=");
      if (shouldBeUser[0].equals("user") && shouldBeMessage[0].equals("message")) {
        String user = shouldBeUser[1];
        String message = shouldBeMessage[1];
        this.chatHistory += user + ": " + message + "\n\n";
        return this.chatHistory;
      } else {
        return "Invalid parameters: " + String.join("&", params);
      }
    }
    // expect /retrieve-history?file=<name>
    else if (url.getPath().equals("/retrieve-history")) {
      String[] params = url.getQuery().split("&");
      String[] shouldBeFile = params[0].split("=");
      if (shouldBeFile[0].equals("file")) {
        String fileName = shouldBeFile[1];
        // String fileName = shouldBeFileName[0]; // bug4: should be shouldBeFile[1]
        ChatHistoryReader reader = new ChatHistoryReader();
        try {
          String[] contents = reader.readFileAsArray("chathistory/" + fileName);
          for (String line : contents) {
            this.chatHistory += line + "\n\n";
          }
        } catch (IOException e) {
          System.err.println("Error reading file: " + e.getMessage());
        }
      }
      return this.chatHistory;
    }
    // expect /save?name=<name>
    else if (url.getPath().equals("/save")) {
      String[] params = url.getQuery().split("&");
      String[] shouldBeFileName = params[0].split("=");
      if (shouldBeFileName[0].equals("name")) {
        File directory = new File("chathistory");
        File file = new File(directory, shouldBeFileName[1]);

        try (BufferedWriter writer = new BufferedWriter(new FileWriter(file))) {
          writer.write(this.chatHistory);
          return "Data written to " + shouldBeFileName[1] + "in 'chat-history' folder.";
        } catch (IOException e) {
          e.printStackTrace();
          return "Error: Something wrong happen during file save, check StackTrace";
        }
      }
    }

    return "404 Not Found";
  }
}

class ChatServer {
  public static void main(String[] args) throws IOException {
    int port = Integer.parseInt(args[0]);
    Server.start(port, new ChatHandler());
  }
}
```
Here is the bash file used to compile the tests:
```
set -e

javac -cp ".;lib/hamcrest-core-1.3.jar;lib/junit-4.13.2.jar" *.java

java -cp ".;lib/junit-4.13.2.jar;lib/hamcrest-core-1.3.jar" org.junit.runner.JUnitCore HandlerTests
```
And the bash file used to run the server:
```
set -e

javac ChatServer.java Server.java

java ChatServer 4000
```
To fix the tests and make them pass, the student edited the failing `handleRequestMulti()` test method and changed the following problematic lines:
```
String url1 = "http://localhost:4000/chat?name=onat&message=good%20luck";
String url2 = "http://localhost:4000/chat?name=edwin&message=with%20your%20demo!";
```
The test was using these URLs to test the methods inside `ChatServer.java`, but these URLs did not follow the proper syntax of the program in declaring a user name for the message. The program uses `user` as the parameter for this, not `name`; as such, to change this so that it works, the URLs needed to be changed to use `user` as the first parameter as follows:

```
String url1 = "http://localhost:4000/chat?name=onat&message=good%20luck";
String url2 = "http://localhost:4000/chat?name=edwin&message=with%20your%20demo!";
```

With this change, the tests passed and the expected behavior was achieved, indicating a productive debugging session!

## Part 2: Reflection:

In this second half of the quarter, I think one of the things that I found very interesting to learn was how to make our own autograder. I thought that I wouldn't be able to even comprehend how something like Gradescope grades our PAs or how TAs and tutors set up autograders using test files and checking for a multitude of different things. Now I know how to use a bash script to do things such as use tester files, check for the presence of certain files, and check for compilation and turn all of those checks into a score I can give a programming assignment. That made the class 100% worth taking for me, and I appreciate that.



## Lab Report 2

# Part 1: Chat Server

Here is the code for my chat server in the folder ChatServer.java:

```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;

class ChatHandler implements URLHandler {

    List<String> chatMessages = new ArrayList<>();

    public String handleRequest(URI url) {
        if (url.getPath().equals("/add-message")) {
            String queryString = url.getQuery();
            String[] parameters = queryString.split("&");

            String str = null;
            String user = null;


            for (String parameter : parameters) {
                String[] strUser = parameter.split("=");
                if (strUser.length == 2) {
                    if (strUser[0].equals("s")) {
                        str = strUser[1];
                    } else if (strUser[0].equals("user")) {
                        user = strUser[1];
                    }
                }
            }

            if (str != null && user != null) {

                String chatMessage = user + ": " + str;
                chatMessages.add(chatMessage);

                return String.join("\n", chatMessages);
            } else {
                return "Error! Missing 'str' or 'user' parameter.";
            }
        } else {
            return "404 Not Found!";
        }
    }
}

public class ChatServer {
    public static void main(String[] args) throws IOException {
        if (args.length == 0) {
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new ChatHandler());
    }
}
```

Here is my first usage of /add-message using path URL `http://localhost:4000/add-message?s=hello&user=bossman`:


<img width="262" alt="Capture" src="https://github.com/kuigi/cse15l-lab-reports/assets/121076589/0fc6cf1f-741d-4934-86ce-e9d18cf372f0">

In this case, the method called was the `handleRequest()` method, which took in the URL that I 
inputted and used the path of that URL to first find that we wanted to use the path `/add-message`. Then, 
using the arguments of the path, it splits the parameter into two parameters: string `str` and user `user`.
In this case, the string or message inputted was "hello" and the user was "bossman". These arguments get
saved in the ArrayList chatMessages, and the result of this first URL is printed.
This leads to the result that we get printed on the website.

This next usage uses the same server (and thus has the saved message from before) and adds one new "chat" using 
the /add-message path at `http://localhost:4000/add-message?s=sup&user=swaglord`:

![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/8a1fa80f-20f2-4164-9134-9b00d460ec6f)

Similar to the last case: 
the method called was the `handleRequest()` method, which took in the URL that I 
inputted and used the new path of that URL to find that we wanted to use the path `/add-message`. Then, 
using the arguments of the path, it splits the parameter into two parameters: string `str` and user `user`.
In this case, the string or message inputted was "sup" and the user was "swaglord". These arguments get
saved in the ArrayList `chatMessages`, and the result of this second URL, as well as the first URL, are printed as the ArrayList chatMessages is printed out in its entirety, resulting in a chat-like print statement.
This leads to the result that we get printed on the website.

## Part 2: SSH Keys with `ls`

For the private key:

![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/00109700-3c34-444b-ba6a-3e7d1e7d60cb)

Above is a screenshot using `ls` with the .ssh directory on my computer's User folder, with the private id_rsa file found at absolute path `C:\Users\Luigi\.ssh\id_rsa`.

For the public key:

![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/0efedc27-f141-41ec-9490-2eedd61c90ca)
Above is a screenshot using `ls` with the .ssh directory containing the file "authorized_keys", which is the saved .pub file I got from my computer. Its file path is `/home/linux/ieng6/oce/1n/lbartulo/.ssh/authorized_keys`.

And here is the terminal not asking me for a password after I log into the ieng6 account:

![image](https://github.com/kuigi/cse15l-lab-reports/assets/121076589/7978ae66-1598-49b1-bdb0-94a029e0312f)

## Part 3: Something New I Learned

In this lab, something I thought was remarkable to have learned is the basics behind creating a very simple web server and search engine. I had always wondered how URLs worked and how the stuff you add at the end of them are read and translated to different pages or different things created, and now I know.











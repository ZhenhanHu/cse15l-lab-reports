# **Lab Report 2 -- Zhenhan Hu(A17282448)**

---

`
import java.io.IOException;
import java.net.URI;
import java.net.URLDecoder;
import java.io.UnsupportedEncodingException;
import java.util.ArrayList;

class Handler implements URLHandler {
    private static ArrayList<String> users = new ArrayList<String>();
    private static ArrayList<String> messages = new ArrayList<String>();

    public String handleRequest(URI url) {
        if (url.getPath().contains("/add-message")) {
            String[] parameters = url.getQuery().split("&");
            try {
                if (((parameters[0].split("="))[0]).equals("s")) {
                    // messages.add(((parameters[0].split("="))[1]));
                    messages.add(URLDecoder.decode((parameters[0].split("="))[1], "UTF-8"));
                    }
                if (((parameters[1].split("="))[0]).equals("user")) {
                    // users.add(((parameters[1].split("="))[1]));
                    users.add(URLDecoder.decode((parameters[1].split("="))[1], "UTF-8"));
                    }
            } catch (UnsupportedEncodingException e) {
                e.printStackTrace();
            }
            String user_message = "";

            for (int i = 0; i < users.size(); i++) {
                user_message = user_message + users.get(i) + ": " + messages.get(i) + "\n";
            }
            return user_message;
            // return ((parameters[1].split("="))[1]) + ": " + ((parameters[0].split("="))[1]);
        } else {
            return "404 Not Found!";
        }
    }
}

class Lab_report_2 {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
`

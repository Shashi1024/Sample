# Distributed Systems Lab Solutions

This document contains Java implementations for the Distributed Systems lab questions.

**Note:** For Client-Server programs, you must always run the **Server** program first in one terminal, and then run the **Client** program in a separate terminal.

---

## SET-1

### i) Write a JAVA program to implementation of Demo Client Server Connection establishment.

**Server Side: `Server.java`**
```java
import java.io.*;
import java.net.*;

public class Server {
    public static void main(String[] args) {
        try {
            ServerSocket serverSocket = new ServerSocket(5000);
            System.out.println("Server is waiting for connection...");

            Socket socket = serverSocket.accept();
            System.out.println("Client Connected Successfully!");

            serverSocket.close();
        } catch (Exception e) {
            System.out.println(e);
        }
    }
}
```

**Client Side: `Client.java`**
```java
import java.io.*;
import java.net.*;

public class Client {
    public static void main(String[] args) {
        try {
            Socket socket = new Socket("localhost", 5000);
            System.out.println("Connected to Server.");
            socket.close();
        } catch (Exception e) {
            System.out.println(e);
        }
    }
}
```

<br>

### ii) Write a JAVA program to implementation of Bulletin Board.

**Server Side: `BulletinServer.java`**
```java
import java.io.*;
import java.net.*;

public class BulletinServer {
    public static void main(String[] args) throws Exception {
        ServerSocket serverSocket = new ServerSocket(5001);
        System.out.println("Bulletin Board Server is running...");

        while (true) {
            Socket socket = serverSocket.accept();
            DataInputStream dataIn = new DataInputStream(socket.getInputStream());
            
            String message = dataIn.readUTF();
            System.out.println("New Bulletin Post: " + message);
            
            socket.close();
        }
    }
}
```

**Client Side: `BulletinClient.java`**
```java
import java.io.*;
import java.net.*;
import java.util.Scanner;

public class BulletinClient {
    public static void main(String[] args) throws Exception {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter message to post: ");
        String message = scanner.nextLine();

        Socket socket = new Socket("localhost", 5001);
        DataOutputStream dataOut = new DataOutputStream(socket.getOutputStream());
        
        dataOut.writeUTF(message);
        System.out.println("Message posted to board.");
        socket.close();
    }
}
```

---

## SET-2

### i) Write a JAVA program to implementation of Client Server Communication to find factorial of a given number.

**Server Side: `FactorialServer.java`**
```java
import java.io.*;
import java.net.*;

public class FactorialServer {
    public static void main(String[] args) throws Exception {
        ServerSocket serverSocket = new ServerSocket(5002);
        System.out.println("Factorial Server Ready...");
        
        Socket socket = serverSocket.accept();
        DataInputStream dataIn = new DataInputStream(socket.getInputStream());
        DataOutputStream dataOut = new DataOutputStream(socket.getOutputStream());

        int number = dataIn.readInt();
        long factorial = 1;
        for(int i = 1; i <= number; i++) {
            factorial = factorial * i;
        }

        dataOut.writeLong(factorial);
        socket.close();
        serverSocket.close();
    }
}
```

**Client Side: `FactorialClient.java`**
```java
import java.io.*;
import java.net.*;
import java.util.Scanner;

public class FactorialClient {
    public static void main(String[] args) throws Exception {
        Socket socket = new Socket("localhost", 5002);
        DataInputStream dataIn = new DataInputStream(socket.getInputStream());
        DataOutputStream dataOut = new DataOutputStream(socket.getOutputStream());
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter a number: ");
        int number = scanner.nextInt();

        dataOut.writeInt(number);
        long result = dataIn.readLong();
        System.out.println("Factorial is: " + result);

        socket.close();
    }
}
```

<br>

### ii) Write a JAVA program for Tic-tac-Toe game.

**File: `TicTacToe.java`**
```java
import java.util.Scanner;

public class TicTacToe {
    public static void main(String[] args) {
        char[][] board = new char[3][3];
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) board[i][j] = '-';
        }

        Scanner scanner = new Scanner(System.in);
        char currentPlayer = 'X';
        boolean hasWon = false;

        while (!hasWon) {
            printBoard(board);
            System.out.println("Player " + currentPlayer + " enter row (0-2) and col (0-2):");
            int r = scanner.nextInt();
            int c = scanner.nextInt();

            if (r >= 0 && r < 3 && c >= 0 && c < 3 && board[r][c] == '-') {
                board[r][c] = currentPlayer;
                if (checkWin(board, currentPlayer)) {
                    printBoard(board);
                    System.out.println("Player " + currentPlayer + " Wins!");
                    hasWon = true;
                } else {
                    currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
                }
            } else {
                System.out.println("Invalid Move.");
            }
        }
    }

    public static void printBoard(char[][] board) {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) System.out.print(board[i][j] + " ");
            System.out.println();
        }
    }

    public static boolean checkWin(char[][] b, char p) {
        for (int i = 0; i < 3; i++) {
            if (b[i][0]==p && b[i][1]==p && b[i][2]==p) return true;
            if (b[0][i]==p && b[1][i]==p && b[2][i]==p) return true;
        }
        if (b[0][0]==p && b[1][1]==p && b[2][2]==p) return true;
        if (b[0][2]==p && b[1][1]==p && b[2][0]==p) return true;
        return false;
    }
}
```

---

## SET-3

### i) Write a JAVA program to implementation of Domain Name Server.

**Server Side: `DNSServer.java` (UDP)**
```java
import java.io.*;
import java.net.*;

public class DNSServer {
    public static void main(String[] args) throws Exception {
        DatagramSocket serverSocket = new DatagramSocket(5003);
        byte[] receiveData = new byte[1024];
        
        System.out.println("DNS Server is Up...");

        while(true) {
            DatagramPacket receivePacket = new DatagramPacket(receiveData, receiveData.length);
            serverSocket.receive(receivePacket);
            
            String domain = new String(receivePacket.getData(), 0, receivePacket.getLength());
            String ip = "Host Not Found";

            if(domain.equalsIgnoreCase("google.com")) ip = "142.250.190.46";
            else if(domain.equalsIgnoreCase("localhost")) ip = "127.0.0.1";

            InetAddress clientIP = receivePacket.getAddress();
            int clientPort = receivePacket.getPort();
            
            byte[] sendData = ip.getBytes();
            DatagramPacket sendPacket = new DatagramPacket(sendData, sendData.length, clientIP, clientPort);
            serverSocket.send(sendPacket);
        }
    }
}
```

**Client Side: `DNSClient.java` (UDP)**
```java
import java.io.*;
import java.net.*;
import java.util.Scanner;

public class DNSClient {
    public static void main(String[] args) throws Exception {
        Scanner scanner = new Scanner(System.in);
        DatagramSocket clientSocket = new DatagramSocket();
        InetAddress ipAddress = InetAddress.getByName("localhost");

        System.out.print("Enter Domain Name: ");
        String domain = scanner.nextLine();
        byte[] sendData = domain.getBytes();

        DatagramPacket sendPacket = new DatagramPacket(sendData, sendData.length, ipAddress, 5003);
        clientSocket.send(sendPacket);

        byte[] receiveData = new byte[1024];
        DatagramPacket receivePacket = new DatagramPacket(receiveData, receiveData.length);
        clientSocket.receive(receivePacket);

        String ip = new String(receivePacket.getData(), 0, receivePacket.getLength());
        System.out.println("IP Address: " + ip);
        clientSocket.close();
    }
}
```

<br>

### ii) Write a JAVA program to implementation of TCP Client & Server communication.

**Server Side: `TCPServer.java`**
```java
import java.io.*;
import java.net.*;

public class TCPServer {
    public static void main(String[] args) throws Exception {
        ServerSocket serverSocket = new ServerSocket(5004);
        System.out.println("TCP Server Waiting...");
        
        Socket socket = serverSocket.accept();
        DataInputStream dataIn = new DataInputStream(socket.getInputStream());
        
        String clientMsg = dataIn.readUTF();
        System.out.println("Received: " + clientMsg);
        
        socket.close();
        serverSocket.close();
    }
}
```

**Client Side: `TCPClient.java`**
```java
import java.io.*;
import java.net.*;

public class TCPClient {
    public static void main(String[] args) throws Exception {
        Socket socket = new Socket("localhost", 5004);
        DataOutputStream dataOut = new DataOutputStream(socket.getOutputStream());
        
        dataOut.writeUTF("Hello Server!");
        System.out.println("Message sent.");
        
        socket.close();
    }
}
```

---

## SET-4

### i) Write a JAVA program to implementation of Demo Client & Server communication.

*(Standard TCP Connection)*

**Server Side: `DemoServer.java`**
```java
import java.io.*;
import java.net.*;

public class DemoServer {
    public static void main(String[] args) throws Exception {
        ServerSocket serverSocket = new ServerSocket(6000);
        System.out.println("Server listening...");
        Socket socket = serverSocket.accept();
        System.out.println("Connection established.");
        socket.close();
    }
}
```

**Client Side: `DemoClient.java`**
```java
import java.io.*;
import java.net.*;

public class DemoClient {
    public static void main(String[] args) throws Exception {
        Socket socket = new Socket("localhost", 6000);
        System.out.println("Connected.");
        socket.close();
    }
}
```

<br>

### ii) Write a JAVA program to implement date service using RPC.

*(Note: This uses Java RMI. Compile all files, then run `rmiregistry` in the background before running the Server).*

**1. Interface: `DateInterface.java`**
```java
import java.rmi.*;

public interface DateInterface extends Remote {
    public String getDate() throws RemoteException;
}
```

**2. Server: `DateServer.java`**
```java
import java.rmi.*;
import java.rmi.server.*;
import java.util.Date;

public class DateServer extends UnicastRemoteObject implements DateInterface {
    public DateServer() throws RemoteException { super(); }

    public String getDate() { return new Date().toString(); }

    public static void main(String[] args) {
        try {
            java.rmi.registry.LocateRegistry.createRegistry(1099);
            DateServer obj = new DateServer();
            Naming.rebind("DateService", obj);
            System.out.println("Date Server Ready.");
        } catch (Exception e) { System.out.println(e); }
    }
}
```

**3. Client: `DateClient.java`**
```java
import java.rmi.*;

public class DateClient {
    public static void main(String[] args) {
        try {
            DateInterface stub = (DateInterface) Naming.lookup("rmi://localhost/DateService");
            System.out.println("Server Date: " + stub.getDate());
        } catch (Exception e) { System.out.println(e); }
    }
}
```

---

## SET-5

### i) Write a JAVA program to implementation FTP Client & Server.

**Server Side: `FTPServer.java`**
```java
import java.io.*;
import java.net.*;

public class FTPServer {
    public static void main(String[] args) throws Exception {
        ServerSocket serverSocket = new ServerSocket(5005);
        System.out.println("FTP Server Ready...");
        Socket socket = serverSocket.accept();

        DataOutputStream dataOut = new DataOutputStream(socket.getOutputStream());
        
        // Ensure "test.txt" exists in the server directory
        File file = new File("test.txt");
        if(file.exists()){
            FileInputStream fileIn = new FileInputStream(file);
            int ch;
            while ((ch = fileIn.read()) != -1) {
                dataOut.writeInt(ch);
            }
            dataOut.writeInt(-1); // EOF
            fileIn.close();
            System.out.println("File sent.");
        }
        socket.close();
    }
}
```

**Client Side: `FTPClient.java`**
```java
import java.io.*;
import java.net.*;

public class FTPClient {
    public static void main(String[] args) throws Exception {
        Socket socket = new Socket("localhost", 5005);
        DataInputStream dataIn = new DataInputStream(socket.getInputStream());
        
        FileOutputStream fileOut = new FileOutputStream("received_copy.txt");
        
        int ch;
        while ((ch = dataIn.readInt()) != -1) {
            fileOut.write(ch);
        }
        
        System.out.println("File received.");
        fileOut.close();
        socket.close();
    }
}
```

<br>

### ii) Write a JAVA program to implementation of Chat Client & Server communication.

**Server Side: `ChatServer.java`**
```java
import java.io.*;
import java.net.*;
import java.util.Scanner;

public class ChatServer {
    public static void main(String[] args) throws Exception {
        ServerSocket serverSocket = new ServerSocket(5006);
        System.out.println("Chat Server Started...");
        Socket socket = serverSocket.accept();

        DataInputStream dataIn = new DataInputStream(socket.getInputStream());
        DataOutputStream dataOut = new DataOutputStream(socket.getOutputStream());
        Scanner scanner = new Scanner(System.in);

        String msgIn = "", msgOut = "";
        while (!msgIn.equals("stop")) {
            msgIn = dataIn.readUTF();
            System.out.println("Client: " + msgIn);
            
            System.out.print("Server: ");
            msgOut = scanner.nextLine();
            dataOut.writeUTF(msgOut);
        }
        socket.close();
    }
}
```

**Client Side: `ChatClient.java`**
```java
import java.io.*;
import java.net.*;
import java.util.Scanner;

public class ChatClient {
    public static void main(String[] args) throws Exception {
        Socket socket = new Socket("localhost", 5006);
        DataInputStream dataIn = new DataInputStream(socket.getInputStream());
        DataOutputStream dataOut = new DataOutputStream(socket.getOutputStream());
        Scanner scanner = new Scanner(System.in);

        String msgIn = "", msgOut = "";
        while (!msgIn.equals("stop")) {
            System.out.print("Client: ");
            msgOut = scanner.nextLine();
            dataOut.writeUTF(msgOut);
            
            msgIn = dataIn.readUTF();
            System.out.println("Server: " + msgIn);
        }
        socket.close();
    }
}
```
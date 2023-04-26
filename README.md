# Java Journey, 12: File Handling.

Repository #12 on File Handling in Java is focused on understanding how to work with files in Java, including creating, reading, writing, and manipulating files. It covers topics such as file input/output streams, file reading/writing techniques, file permissions, file manipulation, and more. This repository is essential for anyone looking to develop file-based applications in Java.

## Learn the basics of I/O streams and the java.io package

In Java, I/O (Input/Output) streams are used to handle input and output operations. The java.io package provides a set of classes and interfaces for performing I/O operations in Java.

The I/O streams can be classified into two categories: byte streams and character streams. Byte streams handle I/O of raw binary data, while character streams handle I/O of character data.

The java.io package provides several classes for reading and writing data from various sources, including files, network sockets, and memory streams. Some of the commonly used classes in the java.io package are FileInputStream, FileOutputStream, FileReader, FileWriter, BufferedInputStream, BufferedOutputStream, BufferedReader, BufferedWriter, and many more.

Understanding I/O streams and the java.io package is essential for handling file I/O operations in Java.

## Study the use of File class to manipulate files and directories

The File class in Java provides a way to interact with the files and directories on the file system. It is part of the java.io package and provides various methods to create, delete, rename, or retrieve information about files and directories.

To manipulate a file or directory, we first create an instance of the File class, passing the file path as a parameter. Once we have a File object, we can perform operations on it such as checking if it exists, creating a new file, renaming it, and deleting it.

Here are some examples of how to use the File class:

1- Creating a new file:

```bash
File file = new File("filename.txt");
file.createNewFile();
```

2- Checking if a file exists:

```bash
File file = new File("filename.txt");
if (file.exists()) {
    System.out.println("File exists");
} else {
    System.out.println("File does not exist");
}
```

3- Renaming a file:

```bash
File file = new File("filename.txt");
File renamedFile = new File("newfilename.txt");
file.renameTo(renamedFile);
```

4- Deleting a file:

```bash
File file = new File("filename.txt");
file.delete();
```

In addition to working with files, the File class also provides methods to work with directories. We can create a new directory, list the contents of a directory, and delete a directory.

Overall, the File class is a powerful tool for manipulating files and directories in Java.

## Learn about the use of FileInputStream and FileOutputStream for reading and writing binary data

In Java, the FileInputStream and FileOutputStream classes are used to read and write binary data, such as images or audio files, from a file.

FileInputStream is used to open an input stream to read data from a file, while FileOutputStream is used to open an output stream to write data to a file. Both of these classes are part of the java.io package.

Here is an example of using FileInputStream to read a binary file:

```bash
FileInputStream input = null;
try {
    input = new FileInputStream("example.bin");
    int byteRead;
    while ((byteRead = input.read()) != -1) {
        // Process the byte read
    }
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (input != null) {
        try {
            input.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

Similarly, here is an example of using FileOutputStream to write binary data to a file:

```bash
FileOutputStream output = null;
try {
    output = new FileOutputStream("example.bin");
    byte[] data = {0x01, 0x02, 0x03};
    output.write(data);
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (output != null) {
        try {
            output.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

In these examples, we create a new FileInputStream or FileOutputStream object and pass the name of the file we want to read from or write to as a parameter. We then use the read() method to read data from the input stream or the write() method to write data to the output stream. Finally, we close the stream using the close() method to ensure that any resources used by the stream are freed.

## Study the use of BufferedReader and BufferedWriter for reading and writing text data

BufferedReader and BufferedWriter are used to read and write text data efficiently. They are more efficient than using FileReader and FileWriter, especially when dealing with large files.

BufferedReader reads text from a character input stream and stores it in an internal buffer for efficient reading of characters, arrays, and lines. The read() method reads a single character, while the readLine() method reads a line of text.

Example of using BufferedReader to read text data from a file:

```bash
try {
    BufferedReader reader = new BufferedReader(new FileReader("example.txt"));
    String line = reader.readLine();
    while (line != null) {
        System.out.println(line);
        line = reader.readLine();
    }
    reader.close();
} catch (IOException e) {
    e.printStackTrace();
}
```

BufferedWriter writes text to a character output stream and stores it in an internal buffer for efficient writing of characters, arrays, and lines. The write() method writes a single character, while the newLine() method writes a newline character.

Example of using BufferedWriter to write text data to a file:

```bash
try {
    BufferedWriter writer = new BufferedWriter(new FileWriter("example.txt"));
    writer.write("Hello World!");
    writer.newLine();
    writer.write("This is a new line.");
    writer.close();
} catch (IOException e) {
    e.printStackTrace();
}
```

These examples demonstrate the use of BufferedReader and BufferedWriter for reading and writing text data efficiently.

## Learn about the use of ObjectInputStream and ObjectOutputStream for reading and writing objects

In Java, ObjectInputStream and ObjectOutputStream are used to read and write objects to and from files. ObjectInputStream reads objects from an InputStream while ObjectOutputStream writes objects to an OutputStream. These classes can be used to serialize and deserialize objects in Java.

Here is an example of how to use ObjectInputStream and ObjectOutputStream for reading and writing objects:

```bash
public class Person implements Serializable {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}

public class ObjectStreamExample {
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        Person person1 = new Person("John", 30);
        Person person2 = new Person("Jane", 25);

        // Writing objects to a file
        FileOutputStream fos = new FileOutputStream("persons.obj");
        ObjectOutputStream oos = new ObjectOutputStream(fos);
        oos.writeObject(person1);
        oos.writeObject(person2);
        oos.close();
        
        // Reading objects from a file
        FileInputStream fis = new FileInputStream("persons.obj");
        ObjectInputStream ois = new ObjectInputStream(fis);
        Person p1 = (Person) ois.readObject();
        Person p2 = (Person) ois.readObject();
        ois.close();
        
        System.out.println(p1.getName() + " " + p1.getAge()); // Output: John 30
        System.out.println(p2.getName() + " " + p2.getAge()); // Output: Jane 25
    }
}
```

In this example, we define a Person class that implements the Serializable interface. We create two Person objects and write them to a file using ObjectOutputStream. Then we read the objects from the file using ObjectInputStream and print their properties. Note that we need to cast the objects to the Person type when we read them from the file.

## Study the use of RandomAccessFile for random access to data within a file.

RandomAccessFile is a class in Java that provides the ability to randomly access data within a file. It can read and write to a file in a non-sequential order.

Here is an example of how to use RandomAccessFile to read from and write to a file:

```bash
import java.io.IOException;
import java.io.RandomAccessFile;

public class RandomAccessFileExample {
    public static void main(String[] args) throws IOException {
        // Creating a RandomAccessFile object with "rw" mode
        RandomAccessFile file = new RandomAccessFile("example.txt", "rw");

        // Writing to the file
        file.write("Hello, World!".getBytes());

        // Moving the file pointer to the beginning of the file
        file.seek(0);

        // Reading from the file
        byte[] buffer = new byte[14];
        file.read(buffer);

        System.out.println(new String(buffer)); // Output: Hello, World!

        // Updating the content of the file
        file.seek(7);
        file.write("Java".getBytes());

        // Moving the file pointer to the beginning of the file
        file.seek(0);

        // Reading from the file
        buffer = new byte[14];
        file.read(buffer);

        System.out.println(new String(buffer)); // Output: Hello, Java!
        
        // Closing the file
        file.close();
    }
}
```

In this example, we create a RandomAccessFile object with "rw" mode to allow both read and write operations. We write the string "Hello, World!" to the file and then move the file pointer to the beginning of the file using the seek() method.

We then read from the file using the read() method and store the result in a byte array. We print the contents of the byte array to the console.

Next, we move the file pointer to position 7 and write the string "Java" to the file. We then move the file pointer to the beginning of the file and read from the file again. This time, we print "Hello, Java!" to the console.

Finally, we close the file using the close() method.

## Practice with sample code and projects.

Practicing with sample code and projects is a great way to improve your understanding of file handling in Java. There are many resources available online that provide sample code and projects for beginners as well as advanced programmers.

For example, let's consider a simple project of creating a text file and writing some data into it using Java. Here is a sample code that achieves this:

```bash
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;

public class FileHandlingExample {
  public static void main(String[] args) {
    try {
      String data = "This is some sample data to write into file.";
      File file = new File("sampleFile.txt");
      FileWriter fileWriter = new FileWriter(file);
      BufferedWriter bufferWriter = new BufferedWriter(fileWriter);
      bufferWriter.write(data);
      bufferWriter.close();
      System.out.println("Data written successfully into file.");
    } catch (IOException e) {
      System.out.println("An error occurred while writing data into file: " + e.getMessage());
    }
  }
}
```

In this code, we have used the File class to create a new file named sampleFile.txt. We then used the FileWriter and BufferedWriter classes to write data into the file. The BufferedWriter class provides a convenient way to write text data into a file, and it also handles the buffering of data internally, which can help improve performance.

By running this code, you can see that it creates a new file named sampleFile.txt in the same directory as the Java file, and writes the data "This is some sample data to write into file." into the file.

Similarly, you can practice with other file handling operations such as reading data from a file, working with binary data, working with directories, and more. By practicing with sample code and projects, you can gain confidence in your understanding of file handling in Java and develop your programming skills.

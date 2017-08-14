
```java runnable
// { autofold
import static java.nio.file.StandardOpenOption.APPEND;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.Arrays;
import java.util.List;

public class Main {

public static void main(String[] args) throws Exception {

// }

Path file = Paths.get("file.txt");

// Method 1: small files: write raw bytes
byte[] bytes = "1st line\n".getBytes();
Files.write(file, bytes);

// Method 2: small files: write lines
List<String> lines = Arrays.asList(
    "2nd line",
    "3rd line",
    "4th line"
);
Files.write(file, lines, APPEND); // UTF8 by default

// Method 3: big files: write text
try (BufferedWriter writer = Files.newBufferedWriter(file, APPEND)) {
    String line = "5th line";
    writer.write(line, 0, line.length());
    writer.newLine();
}

//{ autofold
    try (BufferedReader reader = Files.newBufferedReader(file)) {
        String line = null;
        while ((line = reader.readLine()) != null) {
            System.out.println(line);
        }
    }
}

}
//}
```

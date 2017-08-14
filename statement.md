
```java runnable
// { autofold
import java.io.BufferedReader;
import java.io.IOException;
import java.io.PrintWriter;
import java.nio.charset.Charset;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.nio.file.StandardOpenOption;
import java.util.Arrays;
import java.util.List;

public class Main {

public static void main(String[] args) throws Exception {

// }

Path file = Paths.get("file.txt");

// Method 1: write raw bytes
byte[] bytes = "1st line".getBytes();
Files.write(file, bytes);

// Method 2: write lines
List<String> lines = Arrays.asList(
    "2nd line",
    "3rd line",
    "4th line"
);
Files.write(file, lines, StandardOpenOption.APPEND); // UTF8 by default

//{ autofold
    try (BufferedReader reader = Files.newBufferedReader(Paths.get("file.txt"), StandardCharsets.UTF_8)) {
        String line = null;
        while ((line = reader.readLine()) != null) {
            System.out.println(line);
        }
    }
}

}
//}
```

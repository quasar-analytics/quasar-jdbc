# Quasar JDBC Driver

Thin JDBC driver for Quasar, supporting query execution by connecting to the Quasar web API.


## Building from Source

**Note:** Requires Java 7.

### Checkout

```bash
git clone git@github.com:quasar-analytics/quasar-jdbc.git
```

### Build

Run the tests and assemble the driver and its dependencies into a single jar:
```bash
sbt assembly
```

## Usage

The Quasar API server must be running and accessible via the network. See
[quasar-analytics/quasar](/quasar-analytics/quasar).

You open a connection using a URL made up of the scheme `quasar`, the
host name and port of the Quasar server, and the path within the Quasar
filesystem where your source files are found.

For example `quasar://localhost:8080/test/`.

### From Java

Add `quasar-jdbc_2.11-0.1-SNAPSHOT.jar` to your classpath.

```java
import java.sql.*;

...

Driver driver = new quasar.jdbc.QuasarDriver();

Connection cxn = driver.connect("quasar://localhost:8080/test/", null);
try {
  Statement stmt = cxn.createStatement();

  ResultSet rs = stmt.executeQuery("select * from zips");
  while (rs.next()) {
    for (int i=1; i <= rs.getColumnCount(); i++) {
      if (i > 1) System.out.print("; ");
      System.out.print(rs.getString(i));
    }
    System.out.println();
  }
}
finally {
  cxn.close();
}
```

Note: error handling and resource cleanup elided above.

### With any JDBC-compatible tool

Configure your tool to use `quasar-jdbc_2.11-0.1-SNAPSHOT.jar`.

Open a connection with a URL like `quasar://localhost:8080/test/`.

Run queries...


## Legal

Copyright &copy; 2014 - 2015 SlamData Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.


Copyright 2014-2015 SlamData Inc.

# Using hardcoded IP addresses is security-sensitive

#### Hardcoding IP addresses is security-sensitive. It has led in the past to the following vulnerabilities:

- [CVE-2006-5901](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2006-5901)
- [CVE-2005-3725](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2005-3725)

####  This will have an impact on the product development, delivery, and deployment:

- The developers will have to do a rapid fix every time this happens, instead of having an operation team change a configuration file.
- It misleads to use the same address in every environment (dev, sys, qa, prod).

#### Sensitive Code Example

```java
String ip = "192.168.12.42"; // Sensitive
Socket socket = new Socket(ip, 6667);
```

#### Compliant Solution

```java
String ip = System.getenv("IP_ADDRESS"); // Compliant
Socket socket = new Socket(ip, 6667);
```



## Exceptions

No issue is reported for the following cases because they are **not considered sensitive**:

- Loopback addresses 127.0.0.0/8 in CIDR notation (from 127.0.0.0 to 127.255.255.255)
- Broadcast address 255.255.255.255
- Non routable address 0.0.0.0
- Strings of the form `2.5.<number>.<number>` as they [often match Object Identifiers](http://www.oid-info.com/introduction.htm) (OID).
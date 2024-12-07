### Basic URL filtering mechanism (w/ Squid Proxy)
https://www.squid-cache.org/Download/ \
https://www.digitalocean.com/community/tutorials/how-to-set-up-squid-proxy-on-ubuntu-20-04 \
Open-source caching and forwarding HTTP proxy server that provides web content filtering, access control, and caching functionalities.

This method (below) blocks specific domains by matching the dstdomain (destination domain) against the domains in blocked_urls.txt. \
`sudo apt-get install squid`

**Set custom blocklist**
`nano blocked_urls.txt`
```sh
.torrent.com
.file-sharing.com
.vpn.com
.proxy.com
```
`sudo nano /etc/squid/squid.conf`
```sh
acl blocked_sites dstdomain "/etc/squid/blocked_urls.txt"
http_access deny blocked_sites
```
`sudo systemctl restart squid`



### Insecure Direct Object References (IDOR)
Occur when an application exposes internal objects (like files, database records, or user IDs) directly without proper access control. \
Vulnerable IDOR Code Example (PHP)
```php
$user_id = $_GET['id'];  
$result = $db->query("SELECT * FROM users WHERE id = $user_id");
echo $result['name'];
#Issue: No verification if id belongs to the authenticated user.
```
```url
https://example.com/profile?id=12345
```

### Cross-Site Scripting (XSS)
unsanitized input allows attackers to inject and execute malicious scripts.

```html
<!DOCTYPE html>
<html>
  <body>
    <!-- User input field
    Proper input sanitization and encoding are missing, making the page vulnerable to XSS. -->
    <input id="comment" value="<script>alert('XSS Exploit!')</script>">

    <!-- Vulnerable code: directly renders input -->
    <script>
      document.write(document.getElementById('comment').value);
    </script>
  </body>
</html>
```

###  Resource Reuse (Memory Views)
https://www.geeksforgeeks.org/memoryview-in-python/ \
Memory view directly interacts with the underlying data, and modifying sensitive_data directly affects the memory view. \
Shared memory resources can lead to exposure if not handled properly.
```python
import numpy as np

# Create a NumPy array (sensitive data)
sensitive_data = np.array([255, 255, 255], dtype=np.uint8)

# Create a memory view (shares memory with original array)
memory_view = memoryview(sensitive_data)

# Modify the original array
sensitive_data[0] = 0

# The memory view reflects changes to the original data
print("Memory View Data:", memory_view.tolist())
# >> Memory View Data: [0, 255, 255]
```

| **Term**       | **Definition**                                                                 |
| -              | -                                                                            |
| **Hot Site**   | Fully equipped, real-time replica; ready for immediate operation.            |
| **Cold Site**  | Basic infrastructure only; requires setup and installation before use.       |
| **Warm Site**  | Partially equipped; needs minor configuration to become operational.         |
| **Mobile Site**| Portable, transportable infrastructure for temporary operations.             


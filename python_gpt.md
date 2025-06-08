
# Mastering Python for DevOps Scripting

Python is a powerhouse for DevOps professionals. From automating repetitive tasks to managing cloud infrastructure, Python's simplicity and vast ecosystem make it ideal for scripting in DevOps workflows. This guide will walk you through core concepts, libraries, and real-world use cases to bridge the gap between basic Python and powerful DevOps scripting.

---

## Core Python Concepts for Scripting

### 1. Variables and Data Types
```python
server_name = "web01"
uptime = 24.7
is_active = True
```

### 2. Control Flow
```python
if is_active:
    print(f"{server_name} is online")
else:
    print(f"{server_name} is offline")
```

### 3. Functions
```python
def restart_service(service_name):
    print(f"Restarting {service_name}...")
```

### 4. Loops
```python
services = ["nginx", "mysql", "redis"]
for service in services:
    restart_service(service)
```

### 5. Error Handling
```python
try:
    open("/etc/nonexistent.conf")
except FileNotFoundError as e:
    print(f"Error: {e}")
```

---

## Key Python Libraries for DevOps

### 1. OS Interaction
```python
import os, subprocess, shutil

print(os.getcwd())
subprocess.run(["systemctl", "status", "nginx"])
shutil.copy("source.txt", "backup/source_backup.txt")
```

### 2. File and Directory Manipulation
```python
import os

for root, dirs, files in os.walk("/var/log"):
    for file in files:
        print(os.path.join(root, file))
```

### 3. JSON/YAML Parsing
```python
import json, yaml

with open("config.json") as f:
    config = json.load(f)

with open("config.yaml") as f:
    config_yaml = yaml.safe_load(f)
```

### 4. HTTP Requests
```python
import requests

response = requests.get("https://api.github.com")
print(response.json())
```

### 5. Cloud SDKs
```python
import boto3

ec2 = boto3.client('ec2')
instances = ec2.describe_instances()
```

---

## DevOps Use Cases with Examples

### 1. Automating Infrastructure Provisioning (AWS EC2)
```python
import boto3

ec2 = boto3.resource('ec2')
instance = ec2.create_instances(
    ImageId='ami-0abcdef1234567890',
    MinCount=1,
    MaxCount=1,
    InstanceType='t2.micro'
)
print("Launched instance: ", instance[0].id)
```

### 2. CI/CD Pipeline Trigger (Jenkins)
```python
import requests

jenkins_url = "http://jenkins.local/job/build-project/build"
response = requests.post(jenkins_url, auth=("user", "token"))
print("Build Triggered: ", response.status_code)
```

### 3. Log Parsing and Analysis
```python
with open("/var/log/syslog") as log:
    errors = [line for line in log if "error" in line.lower()]
print(f"Found {len(errors)} errors")
```

### 4. System Administration
```python
import subprocess

user = "newadmin"
subprocess.run(["useradd", user])
subprocess.run(["passwd", user])
```

### 5. REST API Interaction (Jira)
```python
import requests

url = "https://your-jira-instance.atlassian.net/rest/api/2/issue/"
data = {
    "fields": {
       "project": {"key": "DEMO"},
       "summary": "Automated ticket",
       "description": "Created using Python",
       "issuetype": {"name": "Task"}
   }}
headers = {"Content-Type": "application/json"}

response = requests.post(url, json=data, auth=("user", "api_token"), headers=headers)
print(response.json())
```

---

## Best Practices

### 1. Error Handling and Logging
```python
import logging

logging.basicConfig(level=logging.INFO)
try:
    risky_operation()
except Exception as e:
    logging.error("Operation failed: %s", e)
```

### 2. Virtual Environments
```bash
python3 -m venv env
source env/bin/activate
```

### 3. Argument Parsing
```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument("--service")
args = parser.parse_args()

print(f"Managing {args.service}")
```

### 4. Modular Scripts
```python
# utils.py
def greet(name):
    return f"Hello, {name}"

# main.py
from utils import greet
print(greet("DevOps"))
```

### 5. Secure Credential Handling
- Use environment variables.
- Avoid hardcoding secrets.
- Use tools like AWS Secrets Manager or Vault.

### 6. Testing Scripts
```python
def add(a, b):
    return a + b

def test_add():
    assert add(2, 3) == 5
```
Run using `pytest`:
```bash
pytest test_script.py
```

---

## Conclusion

Python empowers DevOps engineers to automate, integrate, and optimize workflows. By mastering scripting basics, leveraging the right libraries, and applying best practices, you can unlock powerful efficiencies across your DevOps pipeline. Start small, script often, and keep iterating!

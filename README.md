# Python_Bruteforce_Simulation
AIG - Shields Up: Cybersecurity Job Simulation

As part of the AIG Shields Up Cybersecurity Virtual Experience Program with Forage, I engaged in a section titled "Bypassing Ransomware," which presented a scenario involving a server compromised by the Log4j vulnerability.

🔒 During this exercise, I was tasked with developing a Python script to perform brute-force decryption on files encrypted by ransomware, aiming to bypass the need to pay the ransom.

💡 Leveraging resources such as the rockyou.txt file, a Forage AIG Brute Force starter template, and Visual Studio Code, I customized and implemented a Brute Force script to recover critical files from the encrypted data.

🎯 This approach demonstrated how proactive measures in a real ransomware incident could potentially circumvent the necessity of paying the ransom.

## This script is designed in Python to brute-force decrypt encrypted files by attempting various decryption keys.

###  Import and Define the First Function:

- zf_handle: A handle for the ZIP file.
- zf_handle.extractall(pwd=password): Attempts to extract all contents of the ZIP file using the provided password. If the password is correct, the extraction will succeed.
- password: The parameter used to attempt to decrypt the encrypted ZIP file. The assumption is that the ZIP file is password-protected.

```
from zipfile import ZipFile

def attempt_extract(zf_handle, password):
    try:
        zf_handle.extractall(pwd=password)
        return True
    except:
        return False
```

### Execution:

- Iterate password entries, extract ZIP file using passwords, handle correct and incorrect attempts.
- def main(): The main function described here performs a brute force attack.
- ZipFile('enc.zip'): Opens the ZIP file named 'enc.zip' using the ZipFile class. The context manager (with statement) ensures the file is properly closed after use.
- with open('rockyou.txt', 'rb') as f: Opens a file named 'rockyou.txt' in binary mode. This file is assumed to contain a list of passwords, one per line. The correct password might be in this list.
- for p in f: Iterates over each line in the password file.
- password = p.strip(): Removes leading and trailing whitespaces from the password obtained from the file.
- Inside the loop, attempt_extract is called with the current password. If the extraction is successful (meaning the correct password is found), it prints a message and exits the program. If the password is incorrect, it prints a message indicating that the password is incorrect.
- If no passwords are correct, a message is displayed.
- The if __name__ == "__main__": block ensures that main() runs when the script is executed, but not if it's imported as a module.
```
def main():
    print("[+] Beginning bruteforce ")
    with ZipFile('enc.zip') as zf:
        with open('rockyou.txt', 'rb') as f:
            for p in f:
                password = p.strip()
                if attempt_extract(zf, password):
                    print('[+] Found correct password: %s' % password)
                    exit(0)
                else:
                    print('[-] Incorrect password: %s' % password)

    print("[+] Password not found in list")
    ```

if __name__ == "__main__":
    main() 

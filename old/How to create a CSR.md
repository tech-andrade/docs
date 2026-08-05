---
sidebar_position: 3
---

To generate a CSR using OpenSSL, you can follow the steps below. This process involves creating a private key and then using that key to generate the CSR.

### Create a Private Key

1. Open the terminal or command prompt.
2. Run the following command to generate a 2048-bit private key:

   ```bash bash
   openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048
   ```

   - **private_key.pem**: This is the name of the file where the private key will be saved. You can change the name as needed.
   - **rsa_keygen_bits:2048**: This parameter specifies the key size. 2048 bits is the standard and recommended size.

### Generate the CSR

1. After creating the private key, use the following command to generate the CSR:

   ```bash bash
   openssl req -new -key private_key.pem -out csr.txt
   ```

   - **private_key.pem**: This is the private key file you just generated.
   - **csr.txt**: This is the name of the file where the CSR will be saved. Again, you can change the name as needed.

2. During the execution of this command, you will be prompted to enter some information, such as country name, state, city, organization name, and more. Simply fill in the requested details as prompted.

### Result

You now have two files:

- **private_key.pem**: Your private key, which should be kept secure and **NEVER** shared, not even with us.
- **csr.txt**: Your generated CSR.
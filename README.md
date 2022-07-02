
# Verilog HDL Implementation of A5/1 stream cipher (Encryption Algorithm).

## Job
 Implement A5/1 stream cipher to encrypt a 256x256 grayscale image.

#### Constraints
    1. Clock Frequency = 100 GHz\
    2. 64 bit secret key = “hardware”
    3. 22 bit public key = 22’b11_0100_1110_0001_1001_0001

## Working
 - The three LFSRs X, Y and Z having lengths equal to 19, 22, and 23 bits respectively are reset to 0.
 - Consecutively XORing Secret Key bits in parallel to the feedback of the register. 

     ![1 of 64](https://user-images.githubusercontent.com/77710362/177014169-9f769358-ca41-4db4-86f6-f9beb6aacfbf.png)

     ![2 of 64](https://user-images.githubusercontent.com/77710362/177014173-046e3b52-230b-4a5b-aa41-f7f6a51aee5b.png)
     
     ![3 of 64](https://user-images.githubusercontent.com/77710362/177014189-ea1fcc43-42bc-467f-a6e6-418c0c5b1eb6.png)
     
     ![4 of 64](https://user-images.githubusercontent.com/77710362/177014195-b115f3a0-3ede-448a-b804-1b0f8315b857.png)
     
 
 - Consecutively XORing Public Key bits in parallel to the feedback of the register.
 
     ![1 of 22](https://user-images.githubusercontent.com/77710362/177014208-4a6a75e4-6b2c-4c63-b4df-e2c7bc92f82f.png)
     
     ![2 of 22](https://user-images.githubusercontent.com/77710362/177014212-19d19faf-c18c-4d4f-a963-30cfc4ba0f91.png)  
     
     ![3 of 22](https://user-images.githubusercontent.com/77710362/177014221-3cbc252d-7c0a-459d-b81f-e6262eecfa69.png)

 - Keystream generation:   
     In the generation of keystream (for 256*256 clock cycles), the shifting of registers will be based on a majority function m.

        m = maj(x8, y10, z10)

     - If x8 = m then X shifts
     - If y10 = m then Y shifts
     - If z10 = m then Z shifts

     and the single keystream bit is-
     
        s = x18 ⊕ y21 ⊕ z22          

     ![A5BY1](https://user-images.githubusercontent.com/77710362/177014237-338387dc-07e2-403c-8ea9-1521eb45e014.png)

- Generating Ciphertext:
     
        plaintext ⊕ keystream = ciphertext
        ciphertext ⊕ keystream = plaintext       

## Results
 - Decrypted Image
   ![decrypt](https://user-images.githubusercontent.com/77710362/177014243-24200adb-3578-4740-9faf-5c7fa4cc8771.jpg)
 - Encrypted Image
   ![encrypt](https://user-images.githubusercontent.com/77710362/177014251-d0d4d915-07b9-487b-886f-99e5fb6eb217.jpg)


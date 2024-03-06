from os import urandom

def generate_random_key():
    return urandom(32)  # For AES-256

def generate_random_iv():
    return urandom(16)  # For AES in CBC mode

def pad_data(data):
    padder = padding.PKCS7(128).padder()
    padded_data = padder.update(data) + padder.finalize()
    return padded_data

def encrypt_cbc_aes(data, key, iv):
    cipher = Cipher(algorithms.AES(key), modes.CBC(iv), backend=default_backend())
    encryptor = cipher.encryptor()
    encrypted_data = encryptor.update(pad_data(data)) + encryptor.finalize()
    return encrypted_data

def decrypt_cbc_aes(encrypted_data, key, iv):
    cipher = Cipher(algorithms.AES(key), modes.CBC(iv), backend=default_backend())
    decryptor = cipher.decryptor()
    decrypted_data = decryptor.update(encrypted_data) + decryptor.finalize()
    return decrypted_data

if __name__ == "__main__":
    # Example usage
    plaintext = b"This is a secret message."
    key = generate_random_key()
    iv = generate_random_iv()

    # Encryption in CBC mode
    ciphertext = encrypt_cbc_aes(plaintext, key, iv)

    # Simulate a bit error in P1 (plaintext block 1)
    error_position = 8  # Assuming an error at the 8th bit of P1
    modified_plaintext = bytearray(plaintext)
    modified_plaintext[error_position] = modified_plaintext[error_position] ^ 1

    # Decrypt the modified ciphertext
    decrypted_text_with_error = decrypt_cbc_aes(ciphertext, key, iv)

    # Display results
    print("Original plaintext:", plaintext)
    print("Encrypted ciphertext:", ciphertext)
    print("Simulated error in P1:", modified_plaintext)
    print("Decrypted text with error:", decrypted_text_with_error)
